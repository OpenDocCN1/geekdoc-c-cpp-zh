# 720 Understanding Web Services

```
public bool AddStuff(string stuff)
{
    // Add it here
    return true;
```

and then you call it like:

```
bool DidItWork = AddStuff("This is the new Stuff");
```

Using Web services, however, you can call the method this way:

```
POST /Service.asmx HTTP/1.1
Host: localhost
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length
<?xml version="1.0" encoding="utf-8"?>
<soap2:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema" xmlns:soap2="http://www.w3.org/2003/05/soap-envelope">
<soap2:Body>
<AddStuff xmlns="http://tempuri.org/">
<stuff>stuff</stuff>
</AddStuff>
</soap2:Body>
</soap2:Envelope>
```

and then you see a response like this one:

```
HTTP/1.1 200 OK
Content-Type: application/soap+xml; charset=utf-8
Content-Length: length
<?xml version="1.0" encoding="utf-8"?>
<soap2:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema" xmlns:soap2="http://www.w3.org/2003/05/soap-envelope">
<soap2:Body>
<AddStuffResponse xmlns="http://tempuri.org/">
<AddStuffResult boolean="true">AddStuffResult
</AddStuffResponse>
</soap2:Body>
</soap2:Envelope>
```

Whoa! Who would anyone want to build a function that I'm asked you. In the later section "Building Service-Oriented Applications," I answer your questions. For now, I describe some concepts that make web services easier to handle.

Web services can be defined by three basic principles: