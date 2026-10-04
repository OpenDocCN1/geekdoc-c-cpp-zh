# Dealing with Web Servers

A PostBack is a JavaScript function used in place of built-in POST function to send information about the page back to the server.
Looks like this to the client:

```
javascript:WebForm_DoPostBackWithOptions(new WebForm_PostBackOptions(&quot;ctl00$phAmd$btnSave&quot;&quot;&quot;true,&quot;&quot;&quot;&quot;false,false);
```

Quite a change from a URL, huh? What do I mean I go back in time.

# Looking back to how things used to be

Back in the day, web servers supported GETs and POSTS. What's more, they still support GETS and POSTS.

A GET is a request for a page, using just the URL. You can send data in the URI (after a question in the link of text) that you are all sending—nothing from the page itself goes back. A GET request looks like this:

```
/fiddler/updatecheck.asp?isBeta=False HTTP/1.1
User-Agent: Fiddler/2.2.4.6 (.NET 2.0.50727.418; Microsoft Windows NT 6.1; WOW)
Pragma: no-cache
Host: www.fiddler.com
Connection: Close
```

A POST sends values from a form on the page. The form can be invisible, but it has to be there. POSTS are a lot bigger than GETs and have a set format that is hard to navigate at times. Here is an example POST:

```
/feedbackaction.asp HTTP/1.1
Accept: application/x-ms,application/jpeg,application/xml,image/gif,image/jpeg,application/x-msap,application/vnd-ms-excel,application/vnd-mspowerpoint,application/msword,application/x-shockwave-
Refer: http://www.gravity.com/feedback.asp
Accept-Language: en-US
User-Agent: Mozilla/4.0 (compatible; .NET 4.0; Windows NT 6.1; WOW64)
Trident/4.0; SLCC2;.NET CLR 2.0.50727; .NET CLR 3.5.50729; .NET CLR 3.0.10329; Media Center PC 6.0; .NET CLR 1.1.44322; InfoPath/2.
Ofofficeconnector.1:OfficePatch.0
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: deflate
Host: www.gravity.com
Content-Length: 69
Connection: Keep-Alive
Pragma: no-cache
Cookie: ASPSESSIONIDDAATQCRCA=MEJFO1FACPGPOMNOBADPIDLLKH
user=bill&email=bill@example.net&subject=Test&comment=This+is+a+POST
```

All the header variables are there, and then the contents of the form are all linked at the end of the request.

![](bbox=[0.863, 0.319, 0.978, 0.455])