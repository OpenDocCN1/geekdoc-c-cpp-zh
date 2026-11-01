The HTTP method is POST.

The SOAP request is:

```
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <FindCountryAsXml xmlns="http://www.ecubicle.net/webservices/">
      <V4IPAddress>string</V4IPAddress>
    </FindCountryAsXml>
  </soap:Body>
</soap:Envelope>
```

The Content-Length of the SOAP request is the total number of characters of the SOAP request.

The Web service will return the following response:

```
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <FindCountryAsXmlResponse xmlns="http://www.ecubicle.net/webservices/">
      <FindCountryAsXmlResult>xml</FindCountryAsXmlResult>
    </FindCountryAsXmlResponse>
  </soap:Body>
</soap:Envelope>
```

In particular, the result (country) will be enclosed within the block of XML results. You would need to extract it from the XML result.

# Using SOAP 1.2

Using SOAP 1.2 is very similar to using SOAP 1.1. The following shows the SOAP request for SOAP 1.2:

```
POST /iptocountry.asmx HTTP/1.1
Host: www.ecubicle.net
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
  <soap12:Body>
    <FindCountryAsXml xmlns="http://www.ecubicle.net/webservices/">
      <V4IPAddress>string</V4IPAddress>
    </FindCountryAsXml>
  </soap12:Body>
</soap12:Envelope>
```