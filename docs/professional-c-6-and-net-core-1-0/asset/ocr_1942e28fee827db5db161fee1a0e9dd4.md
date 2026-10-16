Let’s have a look at what information the client sends within the HTTP header. To access the HTTP header information, the HttpRequest object defines the Headers property. This is of type IHeaderDictionary, and it contains a dictionary with the name of the header and a string array for the values. Using this information, the GetDiv method created earlier is used to write div elements for the client (code file WebSampleApp/RequestAndResponseSample.cs):

```
public static string GetHeaderInformation(HttpRequest request)
{
    var sb = new StringBuilder();

    IHeaderDictionary headers = request.Headers;
    foreach (var header in request.Headers)
    {
        sb.Append(GetDiv(header.Key, string.Join(";", header.Value)));
    }
    return sb.ToString();
}
```

The results you see depend on the browser you’re using. Let’s compare a few of them. The following is from Internet Explorer 11 on a Windows 10 touch device:

```
Connection: Keep-Alive
Accept: text/html,application/xhtml+xml,image/jxr,*.*
Accept-Encoding: gzip, deflate
Accept-Language: en-Us,en;q=0.8,de-AT;q=0.6,de-DE;q=0.4,de;q=0.2
Host: localhost:5000
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; Touch; rv:11.0)
like Gecko
```

Google Chrome version 47.0 shows this information, including version numbers from AppleWebKit, Chrome, and Safari:

```
Connection: keep-alive
Accept:
text/html,application/xhtml,application/xml;q=0.9,image/webp,*.*

Accept-Encoding: gzip, deflate, sdch
Accept-Language: en-Us;en;q=0.8
Host: localhost:5000
User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64)
AppleWebKit/537.36
(KHTML, like Gecko) Chrome 47.0.2526.80 Safari/537.36
```

And Microsoft Edge comes with this information, including version numbers from AppleWebKit, Chrome, Safari, and Edge:

```
Connection: Keep-Alive
Accept: text/html,application/xhtml+xml,image/jxr,*.*
Accept-Encoding: gzip, deflate
Accept-Language: en-Us,en;q=0.8,de-AT;q=0.6,de-DE;q=0.4,de;q=0.2
Host: localhost:5000
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
AppleWebKit/537.36
(KHTML,
```

What can you get out of this header information?