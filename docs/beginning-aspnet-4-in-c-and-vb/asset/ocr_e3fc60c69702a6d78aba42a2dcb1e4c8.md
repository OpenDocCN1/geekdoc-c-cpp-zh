# Syndication

# WHAT'S IN THIS CHAPTER?

+   - System.ServiceModel.Syndication
+   - Syndication Reader
+   - Syndication Feeds

Do you have some structured data to offer, data that changes from time to time? With many web sites, Really Simple Syndication (RSS) or Atom (another syndication format) allow you to subscribe with feed readers. RSS is an XML format that allows syndicate information. RSS became very popular with blogs. This XML information makes it easy to subscribe to using RSS readers.

Nowadays, RSS is not only used with blogs but with many different data sources, such as online news magazines. Any data that changes from time to time is offered by RSS or by its successor protocol Atom. Microsoft Internet Explorer and Microsoft Outlook include RSS and Atom readers that are integrated into the product.

Windows Communication Foundation (WCF) includes an extension for syndication features in the namespace System.ServiceModel.Syndication. This namespace provides classes that can be used to both read and write RSS and Atom feeds.

This chapter shows you how to create syndication readers, as well as how data can be offered.

# OVERVIEW OF SYSTEM.SERVICEMODEL.SYNDICATION

For syndication you can use the namespace System.ServiceModel.Syndication, which offers classes for syndication in an RSS or Atom format.

With the release of RSS version 2.0, RSS is now the shorthand notation for Really Simple Syndication. In earlier versions, it had the name Resource Description Framework (RDF) Site Summary and Rich Site Summary. The first version of RDF was created by Netscape to describe content of its portal site. It became successful when the New York Times began offering its readers subscriptions to RSS news feeds in 2002.