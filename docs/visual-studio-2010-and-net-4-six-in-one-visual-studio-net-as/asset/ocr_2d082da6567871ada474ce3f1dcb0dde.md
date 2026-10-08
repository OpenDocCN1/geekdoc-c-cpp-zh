As with other Silverlight working methods, WCF only provides asynchronous calls to the server. Here is a very simple WCF service call:

```
var sc = new ServiceReference.ServiceClient();
sc.DoWorkCompleted += (obj, args) => { MessageBox.Show(
  "Do work completed!"); };
sc.DoWorkAsync();
```

# WCF RIA Services

WCF RIA Services (formerly called .NET RIA Services) builds upon of WCF and aims to make data transfer between a .NET server and a Silverlight client as transparent as possible. WCF RIA Services addresses CRUD (Create-Read-Update-Delete) schemas while retaining type safety through the layers. Middle-tier entities have corresponding client-side code generated, along with domain contexts that allow access to data through Language Integrated Query (LINQ). Service methods can also be invoked. The tier can connect to any database provider, including Entity Framework, LINQ-to-SQL, and POCO (Plain Old CLR Objects). RIA Services can connect the client-side LINQ query to the server, and translate to T-SQL for the database layer.

> Essentially, it is possible to write LINQ queries using Intellisense in Silverlight to access the database layer, without breaking the architectural integrity, or introducing hand-composed SQL queries that pose serious security problems.

A common problem with client-server scenarios is that part of the application logic (such as validation) must be duplicated. The validation should run on the client for immediate feedback to the user — but also on the server to ensure that the validation cannot be skipped by a malicious client. WCF RIA Services addresses this situation by using attributes and code sharing. This is possible because the same framework runs on the client and the server (the Silverlight client not have all the .NET libraries, of course), this source code can be shared.

WCF RIA Services also integrates with the ASP.NET membership-provider models. It makes it easy to add a Silverlight application to an existing website with authentication, authorization, and profile requirements, or re-use the proven ASP.NET membership infrastructure — including the management tools — for the Silverlight application.

> If you want to integrate with RIA Services, visit Brad Abrams' blog at http://blogs.msdn.com/brada, or look for the WCF RIA Services section in www.silverlight.net for tutorials, videos, and in-depth articles.