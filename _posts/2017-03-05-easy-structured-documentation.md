---
layout: post
comments: true
published: true
title: Easy structured documentation
categories:
  - documentation
  - knowledge base
---
One of the classic problems arising when developing professionally is how to create documentation about our software in a way that is easily disccoverable and updatable from every developer. We faced this problem and tried some options on the way before settling on the easiest and most approachable option we could find.

#### First solution: Sharepoint

This was the solution implemented when I was hired. It basically boils down to a website where documents can be uploaded in a folder-like structure with permission to upload, read and modify them. While it worked it had some serious problems:

- lack of search across documents
- permissions had  to be requested to an administrator to view documents (this could be avoided by giving read permissions to everyone in truth)
- permission had to be requested to modify documents, even to correct a typo
- finding documents was not easy as they could be there but you could be missing the necessary permissions to see them
- its folder-like structure allowed to organize content in a logical way

#### Second solution: The wiki

In the attempt to solve some of these problems we decided to use a Wiki to write our documentation. While it solved some problems it had some disadvantages:

- we had full text search across all documentation
- permission were not needed allowing everyone to contribute and amend the documentation with full traceability
- a logical organization of the documentation was missing requiring each developer to hand mantain it by using links in every page making it tedious and error-prone

### The final solution

At this point we realized we needed a diferent solution, something allowing us to:

- organizing in a hyerarchical way our documentation easily
- allowing everyone to easily update it

To reach this objective we used [Metalsmith](http://www.metalsmith.io/) to create a git repository containing our documentation written in Markdown. Each time someone edits a page, the repository is built by the CI system and a static site is deployed. The structure of the site reflects exactly the on-disk folder structure allowing the topics organization.

In this configuration no permissions are needed as every edit is reflected in the source control history and can easily be reverted.

If you want to try it you can download a personalizable skeleton at https://github.com/Bjornej/KnowledgeBase. To run it just

    npm install
    node -harmony build.js
    
an your static site will be built.
