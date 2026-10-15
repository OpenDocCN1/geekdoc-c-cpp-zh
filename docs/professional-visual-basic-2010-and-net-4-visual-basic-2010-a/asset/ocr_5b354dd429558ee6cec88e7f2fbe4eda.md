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