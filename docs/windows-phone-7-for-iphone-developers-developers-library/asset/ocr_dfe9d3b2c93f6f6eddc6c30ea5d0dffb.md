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