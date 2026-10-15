administrators, working within their guidelines for network access. If they make only certain ports available, then your applications should use only those ports. Alternately, you may be able to get them to configure the firewalls involved to permit the ports needed by your applications. Thankfully, creating network messages is a bit easier with Visual Basic 2010. The following sections demonstrate how.

# THE SYSTEM.NET NAMESPACE

Most of the functionality used when writing network applications is contained within the `System.Net` and `System.Net.Sockets` namespaces. This chapter covers the following main classes in these namespaces:

+   - `WebRequest` and `WebResponse`, and their subclasses, including `FtpWebRequest`
+   - `WebClient`, the simplified `WebRequest` for common scenarios
+   - `HttpListener`, which enables you to create your own Web server

> There are many more classes, methods, properties, and events included in the `System.Net` and `System.Net.Sockets` namespaces. You can locate the current reference for these namespaces at http://msdn.microsoft.com/library/system.net.aspx as of this writing.

# Web Requests (and Responses)

When most people think of network programming these days, they’re really thinking of communication via a Web server or client. Therefore, it shouldn’t be surprising that there is a set of classes for this communication need. In this case, it is the abstract `WebRequest` class and the associated `WebResponse`. These two classes represent the concept of a request/response communication with a Web server, or similar server. As these are abstract classes — that is, `MustInherit` classes — they cannot be created by themselves. Instead, you create the subclasses of `WebRequest` that are optimized for specific types of communication.

The most important properties and methods of the `WebRequest` class are shown in Table 29-2.

# TABLE 29-2: Significant Properties and Methods of WebRequest

| MEMBER | DESCRIPTION |
|---|---|
| Create | Method used to create a specific type of `WebRequest`. This method uses the URL (either as a string or as an Uri class) passed to identify and create a subclass of `WebRequest`. |
| GetRequestStream | Method that allows access to the outgoing request. This enables you to add additional information, such as `POST` data, to the request before sending. |
| GetResponse | Method used to perform the request and retrieve the corresponding `WebResponse` class. |
| Credentials | Property that enables you to set the user ID and password for the request if they are needed to perform it. |
| Headers | Property that enables you to change or add to the headers for the request. |
| Method | Property used to identify the action for the request, such as `GET` or `POST`. The list of available methods is specific to each type of server. |
| Proxy | Property that enables you to identify a proxy server for the communication if needed. You generally don’t need to set this property, as Visual Basic 2010 detects the settings for Internet Explorer and uses them by default. |
| Timeout | Property that enables you to define the duration of the request before you “give up” on the server. |