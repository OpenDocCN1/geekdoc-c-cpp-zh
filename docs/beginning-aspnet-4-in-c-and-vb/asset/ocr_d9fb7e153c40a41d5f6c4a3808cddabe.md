![](bbox=[0.12, 0.12, 0.92, 0.28])

# SOAP

As mentioned, one way to exchange data with web services is SOAP. This technology had a lot of press when it was first released, especially as Microsoft decided to adopt it for use in the .NET Framework. When you think about it, finding out exactly how SOAP works is a bit like finding out about how HTTP works — interesting, but not essential. Most of the time you don’t have to worry about the format of the exchanges made with web services; they just happen, you get the results you want, and everyone is happy.

For this reason, this section won’t go into a huge amount of depth, but you will see some simple SOAP requests and responses so you can get a feel for what is going on under the hood.

Imagine that you want to call a method in a web service with the following signature:

```
int DoSomething(string stringParam, int intParam)
```

The SOAP headers and body required for this are shown in the following code, with the address of the web service (more on this later) at the top:

```
POST /SomeLocation/myWebService.asmx HTTP/1.1
Host: hostname
Content-Type: text/xml; charset=utf-8
Content-Length: length
SOAPAction: "http://tempuri.org/DoSomething"
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <DoSomething xmlns="http://tempuri.org/">
      <stringParam>string</stringParam>
      <intParam>int</intParam>
    </DoSomething>
  </soap:Body>
</soap:Envelope>
```

The length parameter here specifies the total byte size of the content and varies depending on the values sent in the string and int parameters. Host will also vary, depending on where the web service is located.

The SOAP namespace referenced here defines various elements that you use to build your message. When you send this over HTTP, the actual data sent is slightly different (but related). For example, you could call the preceding method using the simple GET method:

```
GET /SomeLocation/myWebService.asmx/DoSomething?stringParam=string&intParam=int HTTP/1.1
Host: hostname
```

The SOAP response of this method is as follows:

```
HTTP/1.1 200 OK
Content-Type: text/xml; charset=utf-8
Content-Length: length
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <DoSomethingResponse xmlns="http://tempuri.org/">
```