sufficient context, such as hypertext links). This creates an environment where the software system consuming the service has more than normal knowledge of the way the data is stored.

# Diving into the details of REST

REST as a concept is as old as the web, but as a web service implementation, it's fairly new — about as new as SOAP. The largest implementation of REST as a standard is the web itself. CGI is based on the REST interface.

The call to a REST interface is clearly smaller than a SOAP call. Seriously. Look at these two examples:

REST:

```
```
POST /Start.aspx HTTP/1.1
Host: localhost
Content-Type: http; charset=utf-8
http://mydomain.com/start.aspx?id=3
```
```

SOAP:

```
```
POST /Service.asmx HTTP/1.1
Host: localhost
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length

<?xml version="1.0" encoding="utf-8"?>
<soap12:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap12="http://www.w3.org/2003/05/soap-envelope">
<soap12:Body>
<helloWorld xmlns="http://tempuri.org/" />
</soap12:Body>
</soap12:Envelope>
```
```

The XML of SOAP kinda gets in the way.

On the other hand, SOAP has a list of security features. There is a list of transaction features. There is a list of attachment features. SOAP has a lot of features.

REST, not so much. REST has only four features:

+   ♦ GET – Request a resource
+   ♦ PUT – Upload a resource
+   ♦ POST – Submit data
+   ♦ DELETE – Delete resource