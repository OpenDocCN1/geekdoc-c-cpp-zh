> *Check out Chapter 31, "ADO.NET Entity Framework," for more information.*

The project template creates a file `IService1.cs` that contains the contract of the WCF service. The interface contains the `CreateFeed()` method, which returns a `SyndicationFeedFormatter`. Because `SyndicationFeedFormatter` is an abstract class, and the real types returned are either `Atom10FeedFormatter` or `Rss20FeedFormatter`, these types are listed with the `ServiceKnownTypeAttribute`, so the type is known for serialization.

The attribute `WebGet` defines that the operation can be called from a simple HTTP GET request that can be used to request syndication feeds. `WebMessageBodyStyle.Bare` defines that the result (the XML from the syndication feed) is sent as it is without adding an XML wrapper element around it:

```
```csharp
using System.ServiceModel;
using System.ServiceModel.Syndication;
using System.ServiceModel.Web;

namespace Wrox.ProcSharp.Syndication
{
    [ServiceContract]
    [ServiceKnownType(typeof(Atom10FeedFormatter))]
    [ServiceKnownType(typeof(Rss20FeedFormatter))]
    public interface IFormula1Feed
    {
        [OperationContract]
        [WebGet(UriTemplate = "*", BodyStyle = WebMessageBodyStyle.Bare)]
        SyndicationFeedFormatter CreateFeed();
    }
}
```
```

*code snippet SyndicationService/IFormula1Feed.cs*

The implementation of the service is done in the class `Formula1Feed`. Here, a `SyndicationFeed` item is created, and various properties of this class such as `Generator`, `Language`, `Title`, `Categories`, and `Authors` are assigned. The `Items` property is filled from a LINQ query that requests the winners of Formula-1 races of the requested date. The select clause of this query creates a new anonymous type that is filled with a few properties which then is used by a `Select()` method to create a `SyndicationItem` for every winner. With `SyndicationItem`, the `Title` property is assigned to plain text containing the country of the race. The `Content` property is filled with the help of LINQ to XML. `XElement` classes are used to create XHTML code that can be interpreted by the browser. This content shows the date of the race, the country, and the name of the winner.

Depending on the query string to request the syndication, the `SyndicationFeed` is formatted with the `Atom10FeedFormatter` or the `Rss20FeedFormatter`:

```
```csharp
using System;
using System.Linq;
using System.ServiceModel.Syndication;
using System.ServiceModel.Web;
using System.Xml.Linq;

namespace Wrox.ProcSharp.Syndication
{
    public class Formula1Feed : IFormula1Feed
    {
        public SyndicationFeedFormatter CreateFeed()
        {
            DateTime fromDate = DateTime.Today - TimeSpan.FromDays(365);
            DateTime toDate = DateTime.Today;
```
```