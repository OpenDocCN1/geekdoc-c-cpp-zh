# WCF DATA SERVICES

In the previous two chapters, you have seen two of the major data access methods in the .NET Framework: “classic” ADO.NET and the Entity Framework. Deciding when to use one over the other depends on whether you’re working on new code versus existing code, and/or your desire to work with the latest and greatest technologies. In both cases, however, you can choose to access your data using either types specifically designed for each data access technology or your own types. Either way, it is assumed that you’re working on a network, and you can expect a .NET class at the other end. WCF Data Services (formerly ADO.NET Data Services) attempts to change that model. Rather than take a traditional .NET or network model to your data access, WCF Data Services (DS) provides a REST model for your data.

# REST

REST, or REpresentational State Transfer, is an application model first defined by Roy Fielding in his doctoral thesis. While you may have never heard of Roy Fielding in the past, you likely use one of his creations daily; he was one of the principal authors of the HTTP specification. In his thesis, he described a way to create applications that “work the way the Internet works”:

+   - Every piece of data (or resource) is uniquely identified by some address within the system.
+   - You use a consistent interface for accessing these resources.
+   - You process these resources through representations of the resources, in known data formats.
+   - The entire system is stateless.

Applying these principals to the Internet, you can see how they work in action:

+   - Every Web page is defined using a unique URL (Uniform Resource Locator).
+   - The HTTP protocol defines a number of verbs that may be used to act on those URLs. While the two most commonly used verbs are GET and POST, many others are available (e.g., PUT and DELETE).
+   - When you request a specific resource, you receive the content along with the MIME type of that content.
+   - HTTP is very stateless (as many new ASP.NET developers painfully discover).

WCF Data Services provides this mechanism for working with your data. It adds an additional layer to your applications that enables you to manipulate an Entity Framework model (or other data, as you’ll see below) using this RESTful model:

+   - Each query, record, or field within your database can be uniquely identified using a URL, such as http://example.com/PubsService.svc/authors('172-32-1176')
+   - You use the same HTTP verbs to access your data (GET to retrieve an item, POST to insert new records, PUT to update them, and DELETE to delete them).
+   - When requesting data, you receive it in Atom or JSON format.
+   - The entire system remains stateless, typically with optimistic concurrency when changing records.

# Atom and JSON

As described above, the data returned by Data Services is in the form of either Atom or JSON. These are both standard data formats: Atom (an official IETF standard – RFC 4287), while JSON (JavaScript Object Notation) is really just using JavaScript’s object definition syntax.