requests. (Other classes are capable of network access, but WebClient is probably the easiest and simplest to use for web service calls.)

Pulling data from a website using a simple HTTP GET couldn’t possibly be easier. The `DownloadStringAsync` method does just what its name implies—it downloads the contents of a particular URI as a single string asynchronously in the background and, when the download is complete, raises an event and trigger your code to deal with the response, as shown in the following code:

```
public void LoadStuff()
{
    WebClient wc = new WebClient();
    wc.DownloadStringAsync(
        new Uri("http://my.server.com/stuff"));
    wc.DownloadStringCompleted +=
        new DownloadStringCompletedEventHandler(wc_DownloadStringCompleted);
}
void wc_DownloadStringCompleted(object sender,
        DownloadStringCompletedEventArgs e)
{
    StringReader sr = new StringReader(e.Result);
    var reader = XmlReader.Create(sr);
    var document = XDocument.Load(reader);
    // Process the XML document
}
```

One of the most commonly performed web activities is a simple HTTP GET to retrieve data. However, smart clients also send data to RESTful services. Suppose our WP7 application submits a new Customer to a RESTful service via HTTP POST. To do this, we’re going to need a little bit finer-grained control over our web request. We need to set the content type (in this case it will be “text/xml”), we need to change the HTTP method to POST, and we need to convert the XML payload into a stream of bytes that we can place into the body of the HTTP POST. It might sound complicated but, comparing the following code to what needs to be done in iOS to perform similar activities, you should be thankful that it is as simple as it is on WP7.

To get started, we’re going to use the `HttpWebRequest` class, which gives us fine-grained control over the request as we build it:

```
private void foo_Click(object sender, RoutedEventArgs e)
{
    HttpWebRequest request = (HttpWebRequest)
        WebRequest.Create(
            "http://localhost/Chapter15ServiceHost/RESTfulService.svc/
UploadedCustomers");
    request.ContentType = "text/xml";
    request.Method = "POST";
    request.BeginGetRequestStream(
        new AsyncCallback(GetRequestStreamCallback), request);
}
```