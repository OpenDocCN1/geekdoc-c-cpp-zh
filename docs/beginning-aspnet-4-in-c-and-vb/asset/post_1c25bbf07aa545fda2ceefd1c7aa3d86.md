
> *Check out Chapter 31, "ADO.NET Entity Framework," for more information.*

The project template creates a file `IService1.cs` that contains the contract of the WCF service. The interface contains the `CreateFeed()` method, which returns a `SyndicationFeedFormatter`. Because `SyndicationFeedFormatter` is an abstract class, and the real types returned are either `Atom10FeedFormatter` or `Rss20FeedFormatter`, these types are listed with the `ServiceKnownTypeAttribute`, so the type is known for serialization.

The attribute `WebGet` defines that the operation can be called from a simple HTTP GET request that can be used to request syndication feeds. `WebMessageBodyStyle.Bare` defines that the result (the XML from the syndication feed) is sent as it is without adding an XML wrapper element around it:

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

*code snippet SyndicationService/IFormula1Feed.cs*

The implementation of the service is done in the class `Formula1Feed`. Here, a `SyndicationFeed` item is created, and various properties of this class such as `Generator`, `Language`, `Title`, `Categories`, and `Authors` are assigned. The `Items` property is filled from a LINQ query that requests the winners of Formula-1 races of the requested date. The select clause of this query creates a new anonymous type that is filled with a few properties which then is used by a `Select()` method to create a `SyndicationItem` for every winner. With `SyndicationItem`, the `Title` property is assigned to plain text containing the country of the race. The `Content` property is filled with the help of LINQ to XML. `XElement` classes are used to create XHTML code that can be interpreted by the browser. This content shows the date of the race, the country, and the name of the winner.

Depending on the query string to request the syndication, the `SyndicationFeed` is formatted with the `Atom10FeedFormatter` or the `Rss20FeedFormatter`:

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
            string from = WebOperationContext.Current.IncomingRequest.UriTemplateMatch
                .QueryParameters["from"];
            string to = WebOperationContext.Current.IncomingRequest.UriTemplateMatch
                .QueryParameters["to"];

            if (from != null && to != null)
            {
                try
                {
                    fromDate = DateTime.Parse(from);
                    toDate = DateTime.Parse(to);
                }
                catch (FormatException)
                {
                    // keep the default dates
                }
            }

            // Create a new Syndication Feed.
            var feed = new SyndicationFeed();
            feed.Generator = "Pro C# 4.0 Sample Feed Generator";
            feed.Language = "en-us";
            feed.LastUpdatedTime = new DateTimeOffset(DateTime.Now);
            feed.Title = SyndicationContent.CreatePlaintextContent(
                "Formula1 results");
            feed.Categories.Add(new SyndicationCategory("Formula1"));
            feed.Authors.Add(new SyndicationPerson("webchristiannagel.com",
                "Christian Nagel", "http://www.christiannagel.com"));
            feed.Description = SyndicationContent.CreatePlaintextContent(
                "Sample Formula 1");

            using (var data = new Formula1Entities())
            {
                var races = (from racer in data.Racers
                             from raceResult in racer.RaceResults
                             where raceResult.Race.Date > fromDate &&
                                   raceResult.Race.Date < toDate &&
                                   raceResult.Position == 1
                             orderby raceResult.Race.Date
                             select new
                             {
                                 Country = raceResult.Race.Circuit.Country,
                                 Date = raceResult.Race.Date,
                                 Winner = racer.Firstname + " " + racer.Lastname
                             }).ToArray();

                feed.Items = races.Select(race =>
                {
                    return new SyndicationItem
                    {
                        Title = SyndicationContent.CreatePlaintextContent(
                            String.Format("G.P. {0}", race.Country)),
                        Content = SyndicationContent.CreateHtmlContent(
                            new XElement("p",
                                new XElement("h3", String.Format("{0}, {1}",
                                    race.Country,
                                    race.Date.ToShortDateString())),
                                new XElement("b", String.Format("Winner: {0}",
                                    race.Winner))).ToString())
                    };
                });
            }

            // Return ATOM or RSS based on query string
            // rss -> http://localhost:8732/Design_Time_Addresses/SyndicationService/
            // Feed1
            // atom -> http://localhost:8732/Design_Time_Addresses/SyndicationService/
            // Feed1?format=atom
            string query = WebOperationContext.Current.IncomingRequest.UriTemplateMatch.QueryParameters["format"];
            SyndicationFeedFormatter formatter = null;
            if (query == "atom")
            {
                formatter = new Atom10FeedFormatter(feed);
            }
            else
            {
                formatter = new Rss20FeedFormatter(feed);
            }
            return formatter;
        }
    }
}
```

code snippet SyndicationService/Formula1Feed.cs

When you start the service from within Visual Studio 2010, the WCF Service Host starts up to host the service, and you can see the feed result with the URL parameter ?From=1970/1/1&to=1971/1/1 formatted in Internet Explorer, as shown in Figure 47-4.

![](img/d7d2ffa0a76feaab821930e95daace93_1454_0.png)

## FIGURE 47-4

With the default request to the service, the RSS feed is returned. An extract of the RSS feed with the rss root element follows. With RSS, the Title property is translated to the title element, and the Description property goes to the description element. The Authors property of the SyndicationFeed

that contains SyndicationPerson uses the e-mail address to create the managingEditor element. With RSS, the content of the item's description element is encoded:

```xml
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
<channel>
<title>Formula1 results</title>
<description>Sample Formula 1</description>
<language>en-us</language>
<managingEditor>web@christiannagel.com</managingEditor>
<lastBuildDate>Sat, 25 Jul 2009 11:25:31+0200</lastBuildDate>
<category>Formula1</category>
<generator>Pro C# 4.0 Sample Feed Generator</generator>
<item>
<title>G.P. South Africa</title>
<description><![CDATA[<p><h3>&#xD; alt:&#xD; alt:h3&gt;South Africa, 07.03.1970&lt;/h3&gt;
&#xD; alt:&#xD; alt:Winner: Jack Brabham&lt;/br&gt;&#xD; alt:&#xD; alt:/p&gt;]]></description>
</item>
<item>
<!-- -->
</channel>
</rss>
```

An Atom-formatted feed is returned with the query ?from=1970/1/1&to=1971/1/1&format=atom with the result shown. The root element now is the feed element; the Description property turns into a subtitle element; and the values for the Author property are now shown completely differently from the RSS feed shown earlier. Atom allows the content to be unencoded. You can easily find the XHTML elements:

```xml
<feed xml:lang="en-us" xmlns="http://www.w3.org/2005/Atom">
<title type="text">Formula1 results</title>
<subtitle type="text">Sample Formula 1</subtitle>
<id>uuid:c1928e67-a4b0-4bc2-9be8-f1960b0f74e7;id=1</id>
<updated>2009-07-25T11:44:01:02:00</updated>
<category term="Formula1"/>
<author>
<name>Christian Nagel</name>
<uri>http://www.christiannagel.com</uri>
<email>web@christiannagel.com</email>
</author>
<generator>Pro C# 4.0 Sample Feed Generator</generator>
<entry>
<id>uuid:c1928e67-a4b0-4bc2-9be8-f1960b0f74e7;id=2</id>
<title type="text">G.P. South Africa</title>
<updated>2009-07-25T09:44:05Z</updated>
<content type="xhtml">
<p><h3>South Africa, 07.03.1970</h3><b>Winner: Jack Brabham</b></p>
</content>
</entry>
<!-- -->
</feed>
```

## SUMMARY

In this chapter, you have seen how the classes from the System.ServiceModel.Syndication namespace can be used to create an application that receives a feed, as well as an application that offers a feed. The syndication API supports RSS 2.0 and Atom 1.0. As syndication standards emerge, new formatters will be available. You have seen that the SyndicationXXX classes are independent of the format that is generated.
