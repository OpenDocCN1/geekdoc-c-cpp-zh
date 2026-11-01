```
```csharp
string from = WebOperationContext.Current.IncomingRequest.UriTemplateMatch
    .QueryParameters[&quot;from&quot;];
string to = WebOperationContext.Current.IncomingRequest.UriTemplateMatch
    .QueryParameters[&quot;to&quot;];

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
feed.Generator = &quot;Pro C# 4.0 Sample Feed Generator&quot;;
feed.Language = &quot;en-us&quot;;
feed.LastUpdatedTime = new DateTimeOffset(DateTime.Now);
feed.Title = SyndicationContent.CreatePlaintextContent(
    &quot;Formula1 results&quot;);
feed.Categories.Add(new SyndicationCategory(&quot;Formula1&quot;));
feed.Authors.Add(new SyndicationPerson(&quot;webchristiannagel.com&quot;,
    &quot;Christian Nagel&quot;, &quot;http://www.christiannagel.com&quot;));
feed.Description = SyndicationContent.CreatePlaintextContent(
    &quot;Sample Formula 1&quot;);

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
                     Winner = racer.Firstname + &quot; &quot; + racer.Lastname
                 }).ToArray();

    feed.Items = races.Select(race =>
    {
        return new SyndicationItem
        {
            Title = SyndicationContent.CreatePlaintextContent(
                String.Format(&quot;G.P. {0}&quot;, race.Country)),
            Content = SyndicationContent.CreateHtmlContent(
                new XElement(&quot;p&quot;,
                    new XElement(&quot;h3&quot;, String.Format(&quot;{0}, {1}&quot;,
                        race.Country,
                        race.Date.ToShortDateString())),
                    new XElement(&quot;b&quot;, String.Format(&quot;Winner: {0}&quot;,
                        race.Winner))).ToString())
        };
    });
}

// Return ATOM or RSS based on query string
```
```