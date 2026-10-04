# 660 Dealing With Web Services

# From the post to the PostBack

Having to handle the header had a lot of problems when it came to the sophisticated web forms that ASP.NET provides, so Microsoft used JavaScript to short-circuit the process. It created a special method that would be on every page that ASP.NET generates.

This method formats the input in order to manage the communication. A PostBack looks like this:

```
/admin/Pages/Add_entry.aspx?id=e87ac8b-1292-4c75-985f-5e85db3089a/HTTP/1.1
Accept: application/x-ms,image/jpeg,application/xml+xml,image/gif,image/jpeg,application/x-ms,application/vnd.ms-excel,
application/vnd.ms-postback,application/msword,application/x-shockwave/*
Referer: http://www.smwef.net/admin/Pages/Add_entry.aspx?id=e87ac8b-1292-4c75-985f-5e85db3089a
Accept-Language: en-US
User-Agent: Mozilla/4.0 (compatible; NT 7.0; Windows NP 6.1; Win64)
CLR: .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NETCLR 3.0.30729; Media Center PC 6.0; .NET CLR 1.1.4322; InfoPath:2;
OfficeLiveConnect:1.3; OfficeLivePatch(0.0)
Content-Type: multipart/form-data; boundary=-
Accept-Encoding: zip, deflate
Host: www.smwef.net
Content-Length: 0399
Connection: Keep-Alive
Pragma: no-cache
```

```
--------------------------------------7d922c32b0016
Content-Disposition: form-data; name="_LASTFOCUS"

----------------------------------------------------------------------
```

```
C# 4.0 at CONIG
--------------------------------------7d922c32b0016
Content-Disposition: form-data; name="ct100$cphAdmin$txtTitle"
```

```
Admin:
--------------------------------------7d922c32b0016
Content-Disposition: form-data; name="ct100$cphAdmin$txtDate"
```

```
2009-09-08 22:21
--------------------------------------7d922c32b0016
Content-Disposition: form-data; name="ct100$cphAdmin$txtContent$txtContentent"
```

<p>I was very pleased to be able to give my C# 4.0 talk at the <a href="http://www.condyg.org/*">Central .NET Developers Group</a> last last month.</p>

```
--------------------------------------7d922c32b0016
Content-Disposition: form-data; name="ct100$cphAdmin$txtUploadImage"; filename="
Content-Type: application/octet-stream
```