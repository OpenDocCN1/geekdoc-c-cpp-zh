# Authentication

Another property in the WebRequest class is the Credentials property. If you need authentication credentials to accompany your request, then you can create an instance of the NetworkCredential class (also from the System.Net namespace) with a username and password. You can place the following code before the call to GetResponse():

```
NetworkCredential myCred = new NetworkCredential("myusername", "mypassword");
wrq.Credentials = myCred;
```

# Working with Proxies

You will find in enterprises that many firms must deal with a proxy server to make any type of HTTP or FTP request. Many times, the proxy server, which routes all the organization's requests and responses, uses some form of security (usually a username and a password). For your applications that use the WebClient or the WebRequest objects, you might need to take these proxy servers into account. As with the preceding NetworkCredential object, you are going to want to use the WebProxy object before you make the actual request:

```
WebProxy wp = new WebProxy("192.168.1.100", true);
wp.Credentials = new NetworkCredential("user1", "user1Password");
WebRequest wrq = WebRequest.Create("http://www.reuters.com");
wrq.Proxy = wp;
WebResponse wrs = wrq.GetResponse();
```

If you require a designation of the user's domain in addition to its credentials, then you would use a different signature on the NetworkCredential instantiation:

```
WebProxy wp = new WebProxy("192.168.1.100", true);
wp.Credentials = new NetworkCredential("user1", "user1Password", "myDomain");
WebRequest wrq = WebRequest.Create("http://www.reuters.com");
wrq.Proxy = wp;
WebResponse wrs = wrq.GetResponse();
```

# Asynchronous Page Requests

An additional feature of the WebRequest class is the ability to request pages asynchronously. This feature is significant because there can be quite a long delay between sending a request to a host and receiving the response. Methods such as WebClient.DownloadData() and WebRequest.GetResponse() will not return until the response from the server is complete. You might not want your application frozen due to a long period of inactivity, and in such scenarios it is better to use the BeginGetResponse() and EndGetResponse() methods. BeginGetResponse() works asynchronously and returns almost immediately. Under the covers, the runtime will asynchronously manage a background thread to retrieve the response from the server. Instead of returning a WebResponse object, BeginGetResponse() returns an object implementing the IAsyncResult interface. With this interface, you can poll or wait for the response to become available and then invoke EndGetResponse() to gather the results.

You can also pass a callback delegate into the BeginGetResponse() method. The target of a callback delegate is a method returning void and accepting an IAsyncResult reference as a parameter. When the worker thread is finished gathering the response, the runtime invokes the callback delegate to inform you of the completed work. As shown in the following code, calling EndGetResponse() in the callback method allows you to retrieve the WebResponse object:

```
public Form1()
{
    InitializeComponent();
    WebRequest wrq = WebRequest.Create("http://www.reuters.com");
```