```
Host: 127.0.0.1::13617
Content-ID: 18

--changeset_8bc1b32a-aceb-400b-9419-dc2eec0e33b7
Content-Type: application/http
Content-Transfer-Encoding: binary

MERGE http://127.0.0.1::13617/RestaurantDataService.svc/Menus(2) HTTP/1.1
Host: 127.0.0.1::13617
Content-ID: 19
Content-Type: application/atom+xml;type=entry
Content-Length: 965

<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<entry xmlns:d="http://schemas.microsoft.com/ado/2007/08/dataservices"
xmlns:m="http://schemas.microsoft.com/ado/2007/08/dataservices/metadata"
xmlns="http://www.w3.org/2005/Atom"
xmlns:category="http://schemas.microsoft.com/ado/2007/08/dataservices/schema"
<category term="RestaurantModel.Menu" />
<title />
<author>
<name />
</author>
<updated>2009-08-01T19:17:43.474188Z</updated>
<id>http://127.0.0.1::13617/RestaurantDataService.svc/Menus(2)</id>
<content type="application/xml">
<m:properties>
<d:Active m:type="Edm.Boolean">true</d:Active>
<d:Description>Lean and tender 8 oz. sirloin seasoned perfectly
with our own special seasonings and topped with seasoned
butter.</d:Description>
<d:Id m:type="Edm.Int32">2</d:Id>
<d:Name>Sirloin Steak</d:Name>
<d:Price m:type="Edm.Decimal">44.0</d:Price>
</m:properties>
</content>
</entry>
--changeset_8bc1b32a-aceb-400b-9419-dc2eec0e33b7--
--batch_244a8a55-e9e1-4e88-853b-cdb5c1dc8bd--
```

# SUMMARY

In this chapter, you've seen the features of WCF Data Services. WCF Data Services brings the data model from the ADO.NET Entity Framework across multiple tiers. The technology that this is based on is WCF, by using connectionless, stateless communication sending AtomPub or JSON queries.

You've not only seen the server-side part of this technology but also the client-side part, where change information is tracked inside a data service context. The client-side part of WCF Data Services implements a LINQ provider, so you can create simple LINQ requests that are converted to HTTP GET/POST/PUT/DELETE requests.