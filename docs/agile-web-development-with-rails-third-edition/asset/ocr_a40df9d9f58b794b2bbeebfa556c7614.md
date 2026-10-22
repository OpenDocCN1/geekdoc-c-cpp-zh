# XML

Many people think that XML is the default choice for building program-to-program protocols over the Web. If used correctly, it can in fact be self-documenting, human-readable, and inherently extensible. And like everything else, not everybody uses it correctly.

XML is best suited for documents, particularly documents that contain markup and/or are persisted on disk. If the document contains primarily markup, consider using XHTML (or even HTML, though some find this harder to parse programmatically).

Although there are no strict limits, XML documents exchanged over the Web tend to range in size from tens of kilobytes to hundreds of megabytes.

The best approach for using XML as a program-to-program protocol is to first get an agreement as to what the XML should look like, capture that in prose or in a schema, and then proceed to writing code that produces or consumes XML, preferably using REXML (or libxml2) and Builder. Extracting data using XPath is an excellent way to keep your clients and servers loosely coupled.

The to_xml method that ActiveRecord provides generally does not help in this circumstance because it makes too many assumptions about how the data will be laid out.

Best practice is to identify each document via a uniform resource identifier (aka a URI; often also referred to as a uniform resource locator, aka a URL) and then provide a uniform interface to this data via the HTTP GET, POST, PUT, and DELETE methods.

The Atom Publishing Protocol, RFC 5023, is an example of this approach. Such approaches scale well to Internet-scale operations.

# JSON

JSON has been growing in popularity in recent years, and some have seen such as a rebuttal to XML. That's true only to the extent that there are people who are preaching XML as a one-size-fits-all strategy, of which there are none.

JSON is best suited for data, particularly for data that already is present inside your application in the form of hashes, arrays, strings, integers, and the like. JSON does not have any direct support for dates or decimals, but Strings or Fixnums will do in a pinch.

Again, there are no strict limits, but JSON is often comfortably deployed in situations where the amount of data is expected to range from a few bytes to several hundred kilobytes. JSON tends to be more compact and faster to parse than XML. There are a few (rare) languages or platforms that don't have ready