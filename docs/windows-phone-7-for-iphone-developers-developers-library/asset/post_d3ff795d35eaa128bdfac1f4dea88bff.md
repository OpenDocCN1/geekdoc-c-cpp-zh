
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

This is the first step in a three-step sequence of asynchronous actions. When the call to BeginRequestStream finishes, it’s going to invoke our callback (other languages refer to this as a completion or a monad, if you’re into that sort of thing). This callback is shown next, which builds the body of the request by converting an XML document into a byte array and then performing the request asynchronously:

```
void GetRequestStreamCallback(IAsyncResult result)
{
    HttpWebRequest request = (HttpWebRequest)result.AsyncState;
    Stream postStream = request.EndGetRequestStream(result);

    string xmlPayload =
        "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
        "<Customer xmlns:xsd=\"http://www.w3.org/2001/XMLSchema\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\">" +
        "<FirstName>Foo</FirstName>" +
        "<LastName>Johnson</LastName>" +
        "<Address>" +
            "<Line1>1 Fake St</Line1>" +
            "<City>FakeVille</City>" +
            "<State>PA</State>" +
            "<Zip>90210</Zip>" +
        "</Address>" +
        "</Customer>";
    byte[] payloadBytes = Encoding.UTF8.GetBytes(xmlPayload);
    postStream.Write(payloadBytes, 0, payloadBytes.Length);
    postStream.Close();
    request.BeginGetResponse(
        new AsyncCallback(GetResponseCallback), request);
}
```

The next step in the chain is the asynchronous callback triggered by the completion of a response. This response could be an error or it could be success. The only way to find out is in the following callback code:

```
void GetResponseCallback(IAsyncResult result)
{
    HttpWebRequest request = (HttpWebRequest)result.AsyncState;
    HttpWebResponse response =
        (HttpWebResponse)request.EndGetResponse(result);
    Stream responseStream = response.GetResponseStream();
    StreamReader streamReader = new StreamReader(responseStream);
    string responseString = streamReader.ReadToEnd();
    Debug.WriteLine(responseString);
    responseStream.Close();
    streamReader.Close();
    response.Close();
}
```

If you’re used to making simple 10-line web service requests in your favorite desktop programming language, don’t be so quick to judge. Just because this way might look different doesn’t mean it’s bad. In fact, after having consumed web services this way (what I call “very asynchronous,” although some refer to it as “ridiculously async”) on WP7 for a while, I’ve actually grown rather fond of it.

During each of these steps, there is a chance for a progress bar or some other visual indication of network activity. If you’ve been using a WP7 device for a while, you are no doubt familiar with the “sliding dots” that appear during most network activity. They are a subtle indicator that some network activity is taking place in the background, but the UI doesn’t get cluttered up with giant wheels or other obtrusive “please wait” or progress indicators.

In addition to being able to provide the user with visual feedback, each of these steps is also a very logical place to trap errors. By taking the little bit of extra time and caution required to implement RESTful web service clients in this fashion, you give your users that feeling of quick, unobtrusive network access that permeates the user experience of all Microsoft’s stock WP7 applications.

Now that you’ve seen how to make simple HTTP GET requests, and you’ve seen how to send XML payloads via HTTP POST, let’s take a look at how incredibly easy it is to parse some data from some of the most popular formats: Twitter, YouTube, and RSS feeds.

First, let’s look at how easy it is to crack open the 10 most recent tweets from a given user (this API access doesn’t require authentication; for more involved Twitter activity you’ll need a developer key):

```
public void LoadTweets()
{
    WebClient wcTweets = new WebClient();
    wcTweets.DownloadStringAsync(new
    Uri("http://api.twitter.com/1/statuses/user_timeline.xml?screen_name=ckindel"));
    wcTweets.DownloadStringCompleted +=
        new DownloadStringCompletedEventHandler(
            wcTweets_DownloadStringCompleted);
}
void wcTweets_DownloadStringCompleted(object sender,
    DownloadStringCompletedEventArgs e)
{
    StringReader sr = new StringReader(e.Result);
    var reader = XmlReader.Create(sr);
    var document = XDocument.Load(reader);

    var tweets =
        from tweet in document.Descendants("status")
        select tweet;
```

```
App.ViewModel.Tweets.Clear();
foreach (var tweet in tweets)
{
    Tweet newTweet = new Tweet
    {
        Text = (string)tweet.Element("text"),
        CreatedAt = DateTime.ParseExact(
            (string)tweet.Element("created_at"),
            "ddd MMM dd HH:mm:ss zz00 yyyy", null)
    };
    App.ViewModel.Tweets.Add(newTweet);
}
TweetsLoaded = true;
```

This code rips through the list of status updates for the user ckindel (Charlie Kindel is a General Manager for the Developer Ecosystem for Windows Phone 7 with Microsoft) and converts them into a view model form to which we can bind a UI. The UI from the sample application for this chapter is shown in Figure 15.1.

![](img/04a00d46bb1059867d95707babd62ee7_214_0.png)

Figure 15.1 Screenshot of smart client application.

And now to sift through the Google Data feed for a particular user's YouTube uploads:

```
public void LoadVideos()
{
    WebClient wc = new WebClient();
    wc.DownloadStringAsync(new Uri("http://gdata.youtube.com/feeds/api/users/thecrochetdude/uploads"));
    wc.DownloadStringCompleted += new DownloadStringCompletedEventHandler(wc_DownloadStringCompleted);
    this.VideosLoaded = true;
}
void wc_DownloadStringCompleted(object sender, DownloadStringCompletedEventArgs e)
{
    StringReader sr = new StringReader(e.Result);
    var reader = XmlReader.Create(sr);
    var document = XDocument.Load(reader);

    XNamespace atom = "http://www.w3.org/2005/Atom";
    var entries =
        from entry in document.Descendants(atom + "entry")
        select entry;

    App.ViewModel.Videos.Clear();
    foreach (var entry in entries)
    {
        App.ViewModel.Videos.Add(new VideoViewModel
        { Title = (string)entry.Element(atom + "title"),
          Description = (string)entry.Element(atom+"content") });
        //Debug.WriteLine(entry.ToString());
        //Debug.WriteLine("Author: " + (string)entry.Element(atom + "author").Element(atom + "name"));
    }
    VideosLoaded = true;
}
```

Here's very similar code (I've skipped the WebClient bit; by now you should be pretty familiar with that part of the code) to convert an RSS feed into instances of view model objects:

```
void wcBlog_DownloadStringCompleted(object sender, DownloadStringCompletedEventArgs e)
{
    StringReader sr = new StringReader(e.Result);
    var reader = XmlReader.Create(sr);
    var document = XDocument.Load(reader);

    var posts =
```
