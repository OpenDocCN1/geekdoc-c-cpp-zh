# Looking back at how things used to be

Back in the day, Web servers supported GETs and POSTs. What's more, they still support GETs and POSTs.

A GET is a request for a page, using the URL. You can send data in the URI (after a question mark in the text of that) but that's all you are sending — nothing from the page itself goes. A GET request looks like this:

```
GET /fiddler/updatecheck.asp?a=False HTTP/1.1
User-Agent: fiddler/2.2.4.6 (.NET 2.0.50272.4918; Microsoft Windows NT 6.1.7100)
Pragma: no-cache
Host: fiddler2.com
Connection: Close
```

A POST sends values from a form. The form can be invisible, but it has to be there. POSTs are a lot bigger than GETs and have a set format that is hard to navigate at times. Here is an example:

```
POST /feedBackAction.asp HTTP/1.1
Accept: application/x-ms-application,image/jpeg,application/xml,image/gif,image/jpeg,application/x-xap,application/vnd/ms-excel,application/vnd/ms-powerpoint,application/msword,application/x-shockwave-flash
Referer: http://www.gravity.com/feedback.asp
Accept-Language: en-us
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64)
Trident/4.0; SLCC; .NET CLR 2.0.50272; .NET CLR 3.5.30429; .NET CLR 1.0.30739; Media Center 6.0; .NET CLR 1.1.4322; InfoPath:2; OfficeLiveConnect.1.3; OfficeLivePatch.0.0
Content-Type: application/x-form-urlencoded
Accept-Encoding: gzip, deflate
Host: www.gravity.com
Content-Length: 69
Connection: Keep-Alive
Pragma: no-cache
Cookie: ASPESSIONIDQATQC=MJEFOIFACPGFONNBDPADLIDKHN
user=bill&email=bill@example.com?subject=Test&comment=This-is+a+POST%21
```

All variables are handled there, and the contents of the form are all linked together at the end of the request.

# From the to PostBack

Having to handle the header had a lot of problems when it came to the sophisticated Web forms that ASP.NET provides, so Microsoft used JavaScript to short-circuit the process. They created a special method that would be on every page that ASP.NET generates.