```
```http
POST /website/multipartupload.aspx HTTP/1.1
Cache-Control: no-cache
Connection: Keep-Alive
Content-Length: 1328
Content-Type: multipart/form-data; boundary="-----------------------------7d44e178b0434"
Accept: */*
Accept-Encoding: gzip, deflate
Host: localhost:60355
User-Agent: Mozilla/5.0 (compatible; MSIE 10.0; Windows NT 6.2; Win64; x64; Trident/6.0; Touch)
UA-CPU: AMD64

-----------------------------7d44e178b0434
Content-Disposition: form-data; name="api_key"

36326323532453245
-----------------------------7d44e178b0434
Content-Disposition: form-data; name="auth_token"

436436545
-----------------------------7d44e178b0434
Content-Disposition: form-data; name="api_sig"

43732850932746573245
-----------------------------7d44e178b0434
Content-Disposition: form-data; name="photo"; filename="tinysquare.jpg"
Content-Type: image/jpeg

(RAW JFIF DATA)
-----------------------------7d44e178b0434--
```
```

To run the sample and also see how this request is received, you'll need two things. First, set up your localhost server as described in "Sidebar: Using the Localhost" in Chapter 4. Then install Visual Studio Express for Web (which is free) through the Web Platform Installer. Now you can go to the MultipartUploadServer folder in appendices' companion content, load website.sln into Visual Studio Express for Web, open MultipartUploadServer.aspx, and set a breakpoint on the first `if` statement inside the `Page_Load` method. Then start the site in the debugger (which runs it in Internet Explorer), which opens that page on a localhost debugging port (and click Continue in Visual Studio when you hit the breakpoint). Copy that page's URL from Internet Explorer for the next step.

Switch to the MultipartUpload example running in Visual Studio for Windows, paste that URI into the URI field, and click the Start Multipart Transfer. When the upload operation's `startAsync` is called, you should hit the server page breakpoint in Visual Studio for Web. You can step through that code if you want and examine the `Request` object; in the end, the code will copy the request into a file named *multipart-request.txt* on that server. This will contain the request contents as above, where you can see the relationship between how you set up the parts in the client and how they are received by the server.