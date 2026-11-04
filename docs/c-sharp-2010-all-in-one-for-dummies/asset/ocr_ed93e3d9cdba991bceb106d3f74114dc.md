# Looking back to how things used to be

Back in the day, Web servers supported GETs and POSTs. What's more, they still support GETs and POSTs.

A GET is a request for a page, using just the URL. You can send data in the URI (after a question mark in the link of text) but that's all you are sending — nothing from the page itself goes back. A GET request looks like this:

```
GET /fiddler2/updatecheck.asp?isBeta=False HTTP/1.1
User-Agent: Fiddler/2.2.4.6 (.NET 2.0.50727.4928; Microsoft Windows NT
6.1.7100.0)
Pragma: no-cache
Host: www.fiddler2.com
Connection: Close
```

A POST sends values from a form on the page. The form can be invisible, but it has to be there. POSTs are a lot bigger than GETs and have a set format that is hard to navigate at times. Here is an example POST.

```
POST /feedbackAction.asp HTTP/1.1
Accept: application/x-ms-application, image/jpeg, application/xaml+xml, image/
gif, image/pjpeg, application/x-ms-xbap, application/vnd.ms-excel,
application/vnd.ms-powerpoint, application/msword, application/x-shockwave-
flash, *
Referer: http://www.groove.com/feedback.asp
Accept-Language: en-US
User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64;
Trident/4.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET
CLR 3.0.30729; Media Center PC 6.0; .NET CLR 1.1.4322; InfoPath.2;
OfficeLiveConnector.1.3; OfficeLivePatch.0.0)
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Host: www.groove.com
Content-Length: 69
Connection: Keep-Alive
Pragma: no-cache
Cookie: ASPSESSIONIDDAQTQCRCA=MJEOIFPACGNOMOBADPIDLKH

user=Bills&email=bill@smf.net&subject=Test&comment=This+is+a+POST&21
```

All the header variables are there, and then the contents of the form are all linked together at the end of the request.

# From the past to the PostBack

Having to handle the header had a lot of problems when it came to the sophisticated Web forms that ASP.NET provides, so Microsoft used JavaScript to short-circuit the process. They created a special method that would be on every page that ASP.NET generates.