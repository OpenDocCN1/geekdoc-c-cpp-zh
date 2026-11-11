```
```http
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.8.1.4)
Host: www.server.com
Accept: text/html, image/gif, image/jpeg, image/png, */*
Accept-Language: en
Accept-Charset: iso-8859-1, utf-8
Cookie: orange=192218887821987
```
```

The setIfModifiedSince method tells the connection that you are only interested in data modified since a certain date.

The setUseCaches and setAllowUserInteraction methods should only be called inside applets. The setUseCaches method directs the browser to first check the browser cache. The setAllowUserInteraction method allows an applet to pop up a dialog box for querying the user name and password for password-protected resources (see Figure 4.7).

![](bbox=[0.107, 0.384, 0.806, 0.804])

**Figure 4.7** A network password dialog box

Finally, you can use the catch-all setRequestProperty method to set any name/value pair that is meaningful for the particular protocol. For the format of the HTTP request headers, see RFC 2616. Some of these parameters are not well documented