
object can be configured with the properties editor to define transactional queues, journal queues, the type of the formatter, the base priority, and so on.

![](img/d7d2ffa0a76feaab821930e95daace93_1446_0.png)

## SUMMARY

In this chapter, you've seen how Message Queuing can be used. Message Queuing is an important technology that offers not only asynchronous, but also disconnected communication. The sender and receiver can be running at different times, which makes Message Queuing an option for smart clients and also useful to distribute the load on the server over time.

The most important classes with Message Queuing are Message and MessageQueue. The MessageQueue class allows sending, receiving, and peeking at messages, and the Message class defines the content that is sent.

WCF offers an abstraction to Message Queuing. You can use the concepts offered by WCF to send messages by calling methods of a proxy and to receive messages by implementing a service.

The next chapter dives into Directory Services, how and when to use these hierarchical data stores, and different ways to connect to this service.

## Syndication

### WHAT'S IN THIS CHAPTER?

- System.ServiceModel.Syndication
- Syndication Reader
- Syndication Feeds

Do you have some structured data to offer, data that changes from time to time? With many web sites, Really Simple Syndication (RSS) or Atom (another syndication format) allow you to subscribe with feed readers. RSS is an XML format that allows syndicate information. RSS became very popular with blogs. This XML information makes it easy to subscribe to using RSS readers.

Nowadays, RSS is not only used with blogs but with many different data sources, such as online news magazines. Any data that changes from time to time is offered by RSS or by its successor protocol Atom. Microsoft Internet Explorer and Microsoft Outlook include RSS and Atom readers that are integrated into the product.

Windows Communication Foundation (WCF) includes an extension for syndication features in the namespace System.ServiceModel.Syndication. This namespace provides classes that can be used to both read and write RSS and Atom feeds.

This chapter shows you how to create syndication readers, as well as how data can be offered.

### OVERVIEW OF SYSTEM.SERVICEMODEL.SYNDICATION

For syndication you can use the namespace System.ServiceModel.Syndication, which offers classes for syndication in an RSS or Atom format.

With the release of RSS version 2.0, RSS is now the shorthand notation for Really Simple Syndication. In earlier versions, it had the name Resource Description Framework (RDF) Site Summary and Rich Site Summary. The first version of RDF was created by Netscape to describe content of its portal site. It became successful when the New York Times began offering its readers subscriptions to RSS news feeds in 2002.

The Atom syndication format was designed to be the successor for RSS and is a proposed standard with RFC 4287: www.ietf.org/rfc/rfc4287.txt. The major difference between RSS and Atom is in the content that can be defined with an item. With RSS, the description element can contain simple text or HTML content in which the reading application does not care about this content. Atom requires that you define a specific type for the content with a type attribute, and it also allows you to have XML content with defined namespaces.

![](img/d7d2ffa0a76feaab821930e95daace93_1449_0.png)

Figure 47-1 shows the logo that is used by RSS and Atom feeds. If a site shows this logo, then an RSS or Atom feed is offered.

The following table lists classes and elements that allow you to create a syndication feed. These classes are independent of the syndication type, RSS or Atom.

| CLASS | DESCRIPTION |
|---|---|
| SyndicationFeed | SyndicationFeed represents the top-level element of a feed. With Atom, the top-level element is <feed>; RSS defines <rss> as the top-level element. With the static method Load(), a feed can be read using an XmlReader. Properties of this class such as Authors, Categories, Contributors, Copyright, Description, ImageUrl, Links, Title, and Items allow you to define child elements. |
| SyndicationPerson | SyndicationPerson represents a person with Name, Email, and Uri that can be assigned to the Authors and Contributors collection. |
| SyndicationItem | A feed consists of multiple items. Some of the properties of an item are Authors, Contributors, Copyright, and Content. |
| SyndicationLink | SyndicationLink represents a link within a feed or an item. This class defines the properties Title and Uri. |
| SyndicationCategory | A feed can group items into categories. The keyword of a category can be set to the Name and Label properties of SyndicationCategory. |
| SyndicationContent | SyndicationContent is an abstract base class that describes the content of an item. Content can be of type HTML, plain text, XHTML, XML, or a URL, described with the concrete classes TextSyndicationContent, UrlSyndicationContent, and XmlSyndicationContent. |
| SyndicationElementExtension | With an extension element, you can add additional content. The SyndicationElementExtension can be used to add information to a feed, a category, a person, a link, and an item. |

To format a feed to the RSS and Atom formats, you can use classes that derive from SyndicationFeedFormatter and SyndicationItemFormatter. With .NET 4, the formatters for feeds are Atom10FeedFormatter and Rss20FeedFormatter, and for items are Atom10ItemFormatter and Rss20ItemFormatter.

### READING SYNDICATION FEEDS SAMPLE

The first sample is a Syndication Reader application with a user interface developed with Windows Presentation Format (WPF). The user interface of the WPF application is shown in Figure 47-2.

The DockPanel named content contains a Frame element that binds the Source property to the first link of an item. With that setting, the Frame control uses the web browser control to display the content from the link:

```
<Window x:Class="Wrox.ProCSharp.Syndication.SyndicationReaderWindow"
xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
Title="{Binding Path=Title.Text}" Height="300" Width="450">

<DockPanel x:Name="feedContent">
<Grid DockPanel.Dock="Top">
<Grid.ColumnDefinitions>
<ColumnDefinition Width="50" />
<ColumnDefinition Width="*" />
<ColumnDefinition Width="90" />
</Grid.ColumnDefinitions>
<Label Grid.Column="0" Margin="5">URL:</Label>
<TextBox Grid.Column="1" x:Name="textUrl" MinWidth="150" Margin="5">http://blogs.thinktecture.com/cnagel/rss.aspx</TextBox>
<Button Grid.Column="2" Margin="5" MinWidth="80" Click="OnGetFeed">Get Feed</Button>
</Grid>
<StackPanel Orientation="Vertical" Background="LightGreen" DockPanel.Dock="Top" x:Name="heading">
<Label DockPanel.Dock="Top" Content="{Binding Path=Title.Text}" FontSize="16" />
<Label DockPanel.Dock="Top" Content="{Binding Path=Description.Text}" />
</StackPanel>
<ListBox DockPanel.Dock="Left" ItemsSource="{Binding}" Style="{StaticResource listTitleStyle}" IsSynchronizedWithCurrentItem="True" HorizontalContentAlignment="Stretch" />
<DockPanel x:Name="content" >
<Label DockPanel.Dock="Top" Content="{Binding Path=Description.Text}" />
<Frame Source="{Binding Path=Links[0].Url}" />
</DockPanel>
</Window>
```

code snippet SyndicationReader/SyndicationReader.xaml

### OFFERING SYNDICATION FEEDS SAMPLE

Reading syndication feeds is one scenario in which the Syndication API can be used. Another is to offer a syndication feed to RSS and Atom clients.

For this, Visual Studio 2010 offers the Syndication Service Library template, which you can use to start with. This template defines a reference to the System.ServiceModel library, and adds an application configuration file to define a WCF endpoint.

To offer data for the syndication feed, the ADO.NET Entity Framework is helpful. In the sample application, the Formula-1 database is used, which you can download from the Wrox web site at www.wrox.com with the sample applications for the book. The ADO.NET Entity Data Model item with the name Formula1Model.edmx is added to the project. Here, the tables Racers, RaceResults, Races, and Circuits are mapped to entity classes Racer, RaceResult, Race, and Circuit, as shown in Figure 47-3.

![](img/d7d2ffa0a76feaab821930e95daace93_1451_0.png)

FIGURE 47-3
