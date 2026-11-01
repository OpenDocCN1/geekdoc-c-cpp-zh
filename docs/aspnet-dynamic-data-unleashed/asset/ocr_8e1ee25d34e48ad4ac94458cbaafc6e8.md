# CHAPTER 6

# Page Templates

# IN THIS CHAPTER

+   - Built-in Page Templates
+   - Creating a New Page Template
+   - Custom Page Templates
+   - URL Routing
+   - Page Template Lookup Rules

Implementation of CRUD (Create, Read, Update and Delete) operations has been an ongoing challenge in web applications. The problem is not so much their complexity, but rather a sheer number of the pages that have to be implemented in a typical enterprise application. It is common in web applications to have a separate web page for implementing each type of operation, with one page for editing a particular entity type and another for displaying it in Read-only mode. The resulting number of pages can quickly become unmanageable in enterprise applications that have dozens and sometimes hundreds of entity types.

In traditional ASP.NET WebForms applications, developers sometimes try to address this problem by creating multipurpose pages, such as a single page that allows users to both *create* and *modify* instances of a particular entity type. Visual Studio even offers limited support for creating multipurpose pages by generating the Item, Edit, and Insert templates for FormView controls. Although this approach reduces the overall number of pages in the application, it does so at the cost of significantly increasing complexity of the individual pages.

The ASP.NET MVC framework attempts to solve this problem by offering scaffolding functionality in Visual Studio, which generates separate CRUD pages for a given entity at design time. Although design-time scaffolding helps create the initial version of the CRUD pages, the task of maintaining the generated code falls back onto developers’ shoulders. In a way, the design-time scaffolding solves the problem of supporting CRUD operations by creating a bigger problem of rapidly increasing the number of pages and amount of code developers have to maintain.