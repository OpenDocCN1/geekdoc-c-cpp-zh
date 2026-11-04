content is then read by wrapping the stream returned by GetResponseStream() inside a StreamReader and then calling ReadToEnd(), which returns the entire contents of the stream as a string.

Using the content, the program then searches for a link. It does this by calling FindLink(), which is a static method also defined by MiniCrawler. FindLink() is called with the content string and the starting location at which to begin searching. The parameters that receive these values are htmlstr and startloc, respectively. Notice that startloc is a ref parameter. FindLink() first creates a lowercase copy of the content string and then looks for a substring that matches href="http, which indicates a link. If a match is found, the URI is copied to uri, and the value of startloc is updated to the end of the link. Because startloc is a ref parameter, this causes its corresponding argument to be updated in Main(), enabling the next search to begin where the previous one left off. Finally, uri is returned. Since uri was initialized to null, if no match is found, a null reference is returned, which indicates failure.

Back in Main(), if the link returned by FindLink() is not null, the link is displayed, and the user is asked what to do. The user can go to that link by pressing L, search the existing content for another link by pressing M, or quit the program by pressing Q. If the user presses L, the link is followed and the content of the link is obtained. The new content is then searched for a link. This process continues until all potential links are exhausted.

You might find it interesting to increase the power of MiniCrawler. For example, you might try adding the ability follow relative links. (This is not hard to do.) You might try completely automating the crawler by having it go to each link that it finds without user interaction. That is, starting at an initial page, have it go to the first link it finds. Then, in the new page, have it go to the first link and so on. Once a dead-end is reached, have it backtrack one level, find the next link, and then resume linking. To accomplish this scheme, you will need to use a stack to hold the URIs and the current location of the search within a URI. One way to do this is to use a Stack collection. As an extra challenge, try creating tree-like output that displays the links.

# Using WebClient

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
```