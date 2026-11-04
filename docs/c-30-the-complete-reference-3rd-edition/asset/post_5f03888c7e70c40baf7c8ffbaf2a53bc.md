
content is then read by wrapping the stream returned by GetResponseStream() inside a StreamReader and then calling ReadToEnd(), which returns the entire contents of the stream as a string.

Using the content, the program then searches for a link. It does this by calling FindLink(), which is a static method also defined by MiniCrawler. FindLink() is called with the content string and the starting location at which to begin searching. The parameters that receive these values are htmlstr and startloc, respectively. Notice that startloc is a ref parameter. FindLink() first creates a lowercase copy of the content string and then looks for a substring that matches href="http, which indicates a link. If a match is found, the URI is copied to uri, and the value of startloc is updated to the end of the link. Because startloc is a ref parameter, this causes its corresponding argument to be updated in Main(), enabling the next search to begin where the previous one left off. Finally, uri is returned. Since uri was initialized to null, if no match is found, a null reference is returned, which indicates failure.

Back in Main(), if the link returned by FindLink() is not null, the link is displayed, and the user is asked what to do. The user can go to that link by pressing L, search the existing content for another link by pressing M, or quit the program by pressing Q. If the user presses L, the link is followed and the content of the link is obtained. The new content is then searched for a link. This process continues until all potential links are exhausted.

You might find it interesting to increase the power of MiniCrawler. For example, you might try adding the ability follow relative links. (This is not hard to do.) You might try completely automating the crawler by having it go to each link that it finds without user interaction. That is, starting at an initial page, have it go to the first link it finds. Then, in the new page, have it go to the first link and so on. Once a dead-end is reached, have it backtrack one level, find the next link, and then resume linking. To accomplish this scheme, you will need to use a stack to hold the URIs and the current location of the search within a URI. One way to do this is to use a Stack collection. As an extra challenge, try creating tree-like output that displays the links.

## Using WebClient

Before concluding this chapter, a brief discussion of WebClient is warranted. As mentioned near the start of this chapter, if your application only needs to upload or download data to or from the Internet, then you can use WebClient instead of WebRequest and WebResponse. The advantage to WebClient is that it handles many of the details for you.

WebClient defines one constructor, shown here:

```
public WebClient()
```

WebClient defines the properties shown in Table 25-6. WebClient defines a large number of methods that support both synchronous and asynchronous communication. Because asynchronous communication is beyond the scope of this chapter, only those methods that support synchronous requests are shown in Table 25-7. All methods throw a WebException if an error occurs during transmission.

The following program demonstrates how to use WebClient to download data into a file:

```
// Use WebClient to download information into a file.

using System;
using System.Net;
using System.IO;

class WebClientDemo {
    static void Main() {
        WebClient user = new WebClient();
        string uri = "http://www.McGraw-Hill.com";
        string fname = "data.txt";

        try {
            Console.WriteLine("Downloading data from " +
                uri + " to " + fname);
            user.DownloadFile(uri, fname);
        } catch (WebException exc) {
            Console.WriteLine(exc);
        }

        Console.WriteLine("Download complete.");
    }
}
```

| Property | Description |
|---|---|
| public string BaseAddress { get; set; } | Obtains or sets the base address of the desired URI. If this property is set, then addresses specified by the WebClient methods will be relative to the base address. |
| public RequestCachePolicy CachePolicy { get; set; } | Obtains or sets the policy that determines when the cache is used. |
| public ICredentials Credentials { get; set; } | Obtains or sets authentication information. This property is null by default. |
| public Encoding Encoding { get; set; } | Obtains or sets the character encoding used while transferring strings. |
| public WebHeaderCollection Headers { get; set; } | Obtains or sets the collection of the request headers. |
| public bool IsBusy { get; } | If the request is still transferring information, this property is true. It is false otherwise. |
| public IWebProxy Proxy { get; set; } | Obtains or sets a proxy. |
| public NameValueCollection QueryString { get; set; } | Obtains or sets a query string consisting of name/value pairs that can be attached to a request. The query string is separated from the URI by a ?. If more than one name/value pair exists, then an & separates each pair. |
| public WebHeaderCollection ResponseHeaders { get; } | Obtains a collection of the response headers. |
| public bool UseDefaultCredentials { get; set; } | Obtains or sets a value that determines if default credentials are used for authentication. If true, the default credentials (i.e., those of the user) are used. They are not used if false. |

## TABLE 25-7 The Synchronous Methods Defined by WebClient

| Method | Description |
|---|---|
| public byte[] DownloadData(string uri) | Downloads the information at the URI specified by uri and returns the result in an array of bytes. |
| public byte[] DownloadData(Uri uri) | Downloads the information at the URI specified by uri and returns the result in an array of bytes. |
| public void DownloadFile(string uri, string fname) | Downloads the information at the URI specified by uri and stores the result in the file specified by fname. |
| public void DownloadFile(Uri uri, string fname) | Downloads the information at the URI specified by uri and stores the result in the file specified by fname. |
| public string DownloadString(string uri) | Downloads the information at the URI specified by uri and returns the result as a string. |
| public string DownloadString(Uri uri) | Downloads the information at the URI specified by uri and returns the result as a string. |
| public Stream OpenRead(string uri) | Returns an input stream from which the information at the URI specified by uri can be read. This stream must be closed after reading is completed. |
| public Stream OpenRead(Uri uri) | Returns an input stream from which the information at the URI specified by uri can be read. This stream must be closed after reading is completed. |
| public Stream OpenWrite(string uri) | Returns an output stream to which information can be written to the URI specified by uri. This stream must be closed after writing is completed. |
| public Stream OpenWrite(Uri uri) | Returns an output stream to which information can be written to the URI specified by uri. This stream must be closed after writing is completed. |
| public Stream OpenWrite(string uri, string how) | Returns an output stream to which information can be written to the URI specified by uri. This stream must be closed after writing is completed. The string passed in how specifies how the information will be written. |
| public Stream OpenWrite(Uri uri, string how) | Returns an output stream to which information can be written to the URI specified by uri. This stream must be closed after writing is completed. The string passed in how specifies how the information will be written. |
| public byte[] UploadData(string uri, byte[] info) | Writes the information specified by info to the URI specified by uri. The response is returned. |
| public byte[] UploadData(Uri uri, byte[] info) | Writes the information specified by info to the URI specified by uri. The response is returned. |
| public byte[] UploadData(string uri, string how, byte[] info) | Writes the information specified by info to the URI specified by uri. The response is returned. The string passed in how specifies how the information will be written. |

This program downloads the information at McGrawHill.com and puts it into a file called data.txt. Notice how few lines of code are involved. By changing the string specified by uri, you can download information from any URI, including specific files.
