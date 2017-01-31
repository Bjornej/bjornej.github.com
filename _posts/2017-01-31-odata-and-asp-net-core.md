---
layout: post
comments: true
published: true
title: OData and ASP.NET Core
categories:
  - OData
  - ASP.NET Core
---
At work we're in the process of migrating some applications to ASP.NET Core to take advantage of some of it's features:

- the ability to self host in process without IIS making it perfect to create standalone services
- its design based on dependency injection

While we would love to be able to use the .NET Core version there are too many libraries that have not been ported still so we are forced to run on the full .NET framework and keep an eye on future developments to use the .NET Core framework.

While this solves many problems some libraries that integrated with ASP.NET have not been ported, in our case what was missing was the OData support. Searching online you can found some informations about it:

- https://github.com/OData/WebApi/issues/772
- https://github.com/OData/WebApi/issues/229
- https://github.com/OData/WebApi/issues/744

but all signs point to the porting work being stopped due to other priorities. This was a show stopper for us as we rely on OData to easily connect a React component representing a sorted, paginated and filterable table directly to a data source without having to code all possible queries.

Fortunately we didn't rely on the classic ODataController but instead bound ODataQueryOptions as an action parameter and the built some extension method to apply them and obtain a PageResult (a type representing your data along with the total number of elements in the collection which is necessary to draw a paginated table).

        [HttpGet]
        public PageResult<Person> Teens(ODataQueryOptions opts)
        {
            return dataSource.Persons().Where(x => x.Age < 18).PagedFilter(opts);
        }

The main problem is that this type by default won't bind to the request as this was done in WebAPI from [ODataQueryParameterBindingAttribute](https://www.symbolsource.org/Public/Metadata/NuGet/Project/Microsoft.AspNet.WebApi.OData/5.2.2/Release/.NETFramework,Version=v4.5/System.Web.Http.OData/System.Web.Http.OData/System.Web.Http.OData/OData/ODataQueryParameterBindingAttribute.cs). As the source is easily available thanks to Microsoft new openness we can easily adapt it to an IModelBinder and IModelBinderProvider used by Asp.NET Core


    public class ODataQueryOptionsModelBinder : IModelBinder
    {
        private struct AsyncVoid
        {
        }

        private static MethodInfo _createODataQueryOptions = typeof(ODataQueryOptionsModelBinder).GetMethod("CreateODataQueryOptions");

        private static readonly Task _defaultCompleted = Task.FromResult<AsyncVoid>(default(AsyncVoid));

        public Task BindModelAsync(ModelBindingContext bindingContext)
        {
            if (bindingContext == null)
            {
                throw new ArgumentNullException("bindingContext");
            }
            
            var request = bindingContext.HttpContext.Request;
            if (request == null)
            {
                throw new ArgumentNullException("actionContext");
            }

            var actionDescriptor = bindingContext.ActionContext.ActionDescriptor;
            if (actionDescriptor == null)
            {
                throw new ArgumentNullException("actionDescriptor");
            }


            Type entityClrType = GetEntityClrTypeFromParameterType(actionDescriptor) ?? GetEntityClrTypeFromActionReturnType(actionDescriptor as ControllerActionDescriptor);

            Microsoft.Data.Edm.IEdmModel model = actionDescriptor.GetEdmModel(entityClrType);
            ODataQueryContext entitySetContext = new ODataQueryContext(model, entityClrType);
            ODataQueryOptions parameterValue = CreateODataQueryOptions(entitySetContext, request, entityClrType);
            bindingContext.Result = ModelBindingResult.Success(parameterValue);

            return _defaultCompleted;
        }

        private static ODataQueryOptions CreateODataQueryOptions(ODataQueryContext ctx, HttpRequest req, Type entityClrType) {
            var method = _createODataQueryOptions.MakeGenericMethod(entityClrType);
            var res = method.Invoke(null,new object[] { ctx,req}) as ODataQueryOptions;
            return res;
        }

        public static ODataQueryOptions<T> CreateODataQueryOptions<T>(ODataQueryContext context, HttpRequest request)
        {
            var req = new System.Net.Http.HttpRequestMessage(System.Net.Http.HttpMethod.Get, request.Scheme + "://" + request.Host + request.Path + request.QueryString);
            return new ODataQueryOptions<T>(context, req);
        }

        internal static Type GetEntityClrTypeFromActionReturnType(ControllerActionDescriptor actionDescriptor)
        {
            if (actionDescriptor.MethodInfo.ReturnType == null)
            {
                throw new Exception("Cannot use ODataQueryOptions when return type is null");
            }

            return TypeHelper.GetImplementedIEnumerableType(actionDescriptor.MethodInfo.ReturnType);
        }

        internal static Type GetEntityClrTypeFromParameterType(ActionDescriptor parameterDescriptor)
        {
            Type parameterType = parameterDescriptor.Parameters.First(x => x.ParameterType == typeof(ODataQueryOptions) || x.ParameterType.IsSubclassOf<ODataQueryOptions>()).ParameterType;

            if (parameterType.IsGenericType &&
                parameterType.GetGenericTypeDefinition() == typeof(ODataQueryOptions<>))
            {
                return parameterType.GetGenericArguments().Single();
            }

            return null;
        }
    }
}


the IModelBinderProvider

    public class ODataModelBinderProvider : IModelBinderProvider
    {
        public IModelBinder GetBinder(ModelBinderProviderContext context)
        {
            if (context.Metadata.ModelType.GetTypeInfo() == typeof(ODataQueryOptions) ||
                context.Metadata.ModelType.GetTypeInfo().IsSubclassOf<ODataQueryOptions>())
            {
                return new ODataQueryOptionsModelBinder();
            }

            return null;
        }
    }

and finally register it  in the **ConfigureServices** method

	var mvc = services.AddMvc(options =>{
    	options.ModelBinderProviders.Insert(0, new ODataModelBinderProvider());
    });

