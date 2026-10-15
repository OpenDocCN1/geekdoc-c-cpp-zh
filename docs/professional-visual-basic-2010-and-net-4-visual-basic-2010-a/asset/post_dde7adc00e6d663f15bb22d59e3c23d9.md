
Atom is an XML format that was initially proposed as a “better RSS,” but it has grown into a flexible format for defining objects of any syntax. Figure 12-35 shows an example of this format. The `<content>` element holds the actual data, while the rest of the XML is used to provide metadata (data about the data).

![](img/d99870e80390742f93963da7be0b2e61_508_0.png)

**FIGURE 12-35**

The root element of Atom is either a `<feed>` node, or an `<entry>` node. Feed elements are used to contain multiple entry elements, whereas an entry element represents a single item.

JSON is a subset of JavaScript that has become a popular syntax for passing data across the Internet (see Figure 12-36). It is a very concise format for describing data. Individual objects are wrapped in braces ({}); and within an object, the properties are defined using name:value pairs, each in quotes. Collections are defined by wrapping the child objects with brackets ([]).

![](img/d99870e80390742f93963da7be0b2e61_508_1.png)

**FIGURE 12-36**

The benefit of JSON over Atom is this conciseness. For the single author shown in Figures 12-35 and 12-36, the JSON version is 459 bytes, whereas the Atom format is 1,300 bytes. Obviously, the more objects you have here, the more the XML format would increase this difference. Conversely, the Atom format retains more information about the record than the bare-bones JSON format.

## Exposing Data Using WCF Data Services

WCF Data Services is a specialized WCF library that converts the HTTP requests to some provider. Currently, DS supports the Entity Framework as well as custom objects.

Adding DS support to a project containing an Entity Framework model is as simple as adding a new WCF Data Service class to the project (see Figure 12-37). This adds a new class to the project that represents the actual service:

```
Imports System.Data.Services
Imports System.Linq
Imports System.ServiceModel.Web

Public Class PubsService
  ' TODO: replace [[class name]] with your data class name
  Inherits DataService(Of [[class name]])

  ' This method is called only once to initialize service-wide policies.
  Public Shared Sub InitializeService(ByVal config As IDataServiceConfiguration)
    ' TODO: set rules to indicate which entity sets
    ' and service operations are visible, updatable, etc.
    ' Examples:
    ' config.SetEntitySetAccessRule("MyEntityset", EntitySetRights.AllRead)
    ' config.SetServiceOperationAccessRule("MyServiceOperation",
    ServiceOperationRights.All)
  End Sub

End Class
```

Code snippet from SimpleDataService

![](img/d99870e80390742f93963da7be0b2e61_509_0.png)

FIGURE 12-37

As shown in the preceding code, you must perform a number of steps before the project will compile. First, you need to identify the class providing the data. Second, by default, DS does not allow any data access. You need to explicitly identify the objects that may be queried, and what users may do with them. When exposing an Entity Framework model, the class is your entities. You can apply multiple security rules, depending on how you have separated the entities in your model. Alternately, you can take the easy route and expose all the objects in your model, as shown in the following code:

```
Public Class PubsService
    Inherits DataService(Of PubsEntities)

    ' This method is called only once to initialize service-wide policies.
    Public Shared Sub InitializeService(ByVal config As IDataServiceConfiguration)
        config.SetEntitySetAccessRule("*", EntitySetRights.All)
        config.UseVerboseErrors = True
    End Sub

End Class
```

Once you have configured your data service, you can browse to the service to view the available resources (see Figure 12-38).

![](img/d99870e80390742f93963da7be0b2e61_510_0.png)

FIGURE 12-38

Each of the collections returned represents an additional query you can perform. Figure 12-39 shows the results of querying the authors table.

![](img/d99870e80390742f93963da7be0b2e61_511_0.png)

### FIGURE 12-39

As shown in Table 12-9, you can perform a number of different queries using any browser:

### TABLE 12-9: Query Examples and Results

| QUERY | QUERY EXAMPLE | RESULT |
|---|---|---|
| /entity | /authors | Returns a list of all the entities in that table |
| /entity(KEY) | /authors('213-46-8915') | Returns a single entity, identified by the provided key |
| /entity(KEY)/related | /titles('BU1032')/sales | Returns the data in the related table (in this case, the sales for a specific title) |
| /entity(KEY)/field | /authors('213-46-8915')/address | Returns the data for a specific column (Note: This can be combined with any of the queries to return specific column data.) |
| /entity(multiple keys) | /sales(ord_num='6871', stor_id='6380',title_id='BU1032')/store/ | Returns an item defined by multiple query values |

These queries can be combined, enabling you to extract just the data you want. For example, /sales(ord_num='6871',stor_id='6380',title_id='BU1032')/store/stor_name would return the store name for one specific order of one specific title. When using a browser to explore the data service, the <link> elements in each entry shows you other queries you can perform.

In addition to the entity-specific queries, you can use several additional operators to compose your queries. In each case, the operator can be appended to the query as a query parameter. Some of these parameters are listed in Table 12-10:

**TABLE 12-10:** Operators Used as Query Parameters

| OPERATOR | EXAMPLE |
|---|---|
| `$value` | Returns just the data for a field, without any containing XML. This can be used in much the same way you might query a database to get a single value using `ExecuteScalar`. |
| `$orderby` | Sorts the returned data. You can include multiple sort items by separating them with commas. For example: `/authors/?$orderby=state,city` would sort first by state, then by city to return the authors. Adding “desc” to the end will sort in descending order. |
| `$top, $skip` | Typically used together to enable paging data. `$top` returns the top *n* elements, while `$skip` ignores that many items before returning data. For example, `/authors/?$orderby=state,city&$top=4&$skip=4` would return the second set of four authors. |
| `$expand` | When querying for data that includes child data (e.g., order detail rows when retrieving orders), `$expand` returns the child data as well. |
| `$filter` | Enables you to more flexibly query the data. This includes a number of operations for comparison, string, date and mathematical functions, and more. Some example queries include `/authors/?$filter=(state eq 'CA')`, `/authors/?$filter=startswith(au_lname, 'S')`, and `/sales/?$filter=year(ord_date) gt 1993&$orderby=ord_date desc`. Of course, these can also be combined with the usual AND, OR and NOT operations to create very rich queries. |

Although working with the Data Service using the browser provides you with an easy way to query the data, you are limited in what you can do with it. You cannot query to retrieve the JSON representation, for example. To get more flexibility, you should download the free Fiddler tool (www.fiddlertool.com) to work with DS. This tool provides a great deal of support for working with HTTP, including monitoring request made via a browser, as well as the capability to make requests from Fiddler itself. By adding the `Accept:application/json` header to the request, you can view the JSON output of the data service. Fiddler also enables you to build requests for working with the other HTTP verbs.

Any client that can generate the appropriate URL can query the data service. As the resulting data is in standard data formats, you should be able to work with the data, even on non-.NET clients. The following code shows a simple console application that queries the PubsDataService to retrieve and display a list of the authors, sorted by state and city. The client could be an ASP.NET application, using jQuery or ASP.NET AJAX to retrieve the data, a Silverlight application, a WPF application, or even an application running on another platform.

```
Module Main

    'replace this with the address of your service
    Const ADDRESS As String =
        "http://localhost:49233/PubsService.svc/authors/?$orderby=state,city"

    Sub Main()
        Dim doc As New XDocument()
        Dim schemaNS As XNamespace =
            "http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
        Dim schemaDS As XNamespace =
            "http://schemas.microsoft.com/ado/2007/08/dataservices"

        doc = XDocument.Load(ADDRESS)
        Dim authors = (From prop In doc.Descendants(schemaNS + "properties")
                       From a In prop.Descendants(schemaDS + "au_lname")
```
