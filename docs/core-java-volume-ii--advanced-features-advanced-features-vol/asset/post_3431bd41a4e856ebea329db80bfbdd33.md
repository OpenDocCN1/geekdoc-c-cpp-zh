
## java.net.URLConnection 1.0 *(Continued)*

- `void setIfModifiedSince(long time)`
- `long getIfModifiedSince()`

  The `ifModifiedSince` property configures this `URLConnection` to fetch only data modified since a given time. The time is given in seconds since midnight, GMT, January 1, 1970.

- `void setConnectTimeout(int timeout)` 5.0
- `int getConnectTimeout()` 5.0

  sets or gets the timeout for the connection (in milliseconds). If the timeout has elapsed before a connection was established, the connect method of the associated input stream throws a `SocketTimeoutException`.

- `void setReadTimeout(int timeout)` 5.0
- `int getReadTimeout()` 5.0

  sets or gets the timeout for reading data (in milliseconds). If the timeout has elapsed before a read operation was successful, the read method throws a `SocketTimeoutException`.

- `void setRequestProperty(String key, String value)`

  sets a request header field.

- `Map<String,List<String>> getRequestProperties()` 1.4

  returns a map of request properties. All values for the same key are placed in a list.

- `void connect()`

  connects to the remote resource and retrieves the response header information.

- `Map<String,List<String>> getHeaderFields()` 1.4

  returns a map of response headers. All values for the same key are placed in a list.

- `String getHeaderFieldKey(int n)`

  gets the key for the nth response header field, or null if n is ≤ 0 or greater than the number of response header fields.

- `String getHeaderField(int n)`

  gets value of the nth response header field, or null if n is ≤ 0 or greater than the number of response header fields.

- `int getContentLength()`

  gets the content length if available, or -1 if unknown.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_284_0.png)

**Figure 4.7** An HTML form

The server-side program processes the form data and produces another HTML page that the web server sends back to the browser. This sequence is illustrated in Figure 4.8. The response page can contain new information (for example, in an information-search program) or just an acknowledgment. The web browser then displays the response page.

We do not discuss the implementation of server-side programs in this book. Our interest is merely in writing client programs that interact with existing server-side programs.

When form data are sent to a web server, it does not matter whether the data are interpreted by a servlet, a CGI script, or some other server-side technology. The client sends the data to the web server in a standard format, and the web server takes care of passing it on to the program that generates the response.

Two commands, called GET and POST, are commonly used to send information to a web server.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_285_0.png)

**Figure 4.8** Data flow during execution of a server-side program

In the GET command, you simply attach query parameters to the end of the URL. The URL has the form

```
http://host/path?query
```

Each parameter has the form *name=value*. Parameters are separated by & characters. Parameter values are encoded using the *URL encoding* scheme, following these rules:

- Leave the characters A through Z, a through z, 0 through 9, and . - _ unchanged.
- Replace all spaces with + characters.
- Encode all other characters into UTF-8 and encode each byte by a %, followed by a two-digit hexadecimal number.

For example, to transmit *San Francisco, CA*, you use San+Francisco%2cCA, as the hexadecimal number 2c is the UTF-8 code of the ',' character.

This encoding keeps any intermediate programs from messing with spaces and other special characters.

At the time of this writing, the Google Maps site (www.google.com/maps) accepts query parameters with names q and hl whose values are the location query

> **NOTE:** If cookies need to be sent from one site to another in a redirect, you can configure the global cookie handler like this:
>
> `CookieHandler.setDefault(new CookieManager(null, CookiePolicy.ACCEPT_ALL));`
>
> Then cookies will be properly included in the redirect.

Even though redirects are usually automatically handled, there are some situations where you need to do them yourself. Automatic redirects between HTTP and HTTPS are not supported for security reasons. Redirects can also fail for more subtle reasons. For example, an earlier version of the zip code service used a redirect. Recall that we set the User-Agent request parameter so that the post office didn't think we made a request via the Java API. While it is possible to set the user agent to a different string in the initial request, that setting is not used in automatic redirects. Instead, automatic redirects always send a generic user agent string that contains the word Java.

In such situations, you can manually carry out the redirects. Before connecting the server, turn off automatic redirects:

```
connection.setInstanceFollowRedirects(false);
```

After making the request, get the response code:

```
int responseCode = connection.getResponseCode();
```

Check if it is one of

- `HttpURLConnection.HTTP_MOVED_PERM`
- `HttpURLConnection.HTTP_MOVED_TEMP`
- `HttpURLConnection.HTTP_SEE_OTHER`

In that case, get the Location response header to obtain the URL for the redirect. Then disconnect and make another connection to the new URL:

```
String location = connection.getHeaderField("Location");
if (location != null)
{
   URL base = connection.getURL();
   connection.disconnect();
   connection = (HttpURLConnection) new URL(base, location).openConnection();
   . . .
}
```

The techniques that this program illustrates can be useful whenever you need to query information from an existing web site. Simply find out the parameters that you need to send, and then strip out the HTML tags and other unnecessary information from the reply.

## **Listing 4.7** post/PostTest.java

```java
package post;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.nio.file.*;
import java.util.*;

/**
 * This program demonstrates how to use the URLConnection class for a POST request.
 * @version 1.42 2018-03-17
 * @author Cay Horstmann
 */
public class PostTest
{
   public static void main(String[] args) throws IOException
   {
      String propsFilename = args.length > 0 ? args[0] : "post/post.properties";
      var props = new Properties();
      try (InputStream in = Files.newInputStream(Paths.get(propsFilename)))
      {
         props.load(in);
      }
      String urlString = props.remove("url").toString();
      Object userAgent = props.remove("User-Agent");
      Object redirects = props.remove("redirects");
      CookieHandler.setDefault(new CookieManager(null, CookiePolicy.ACCEPT_ALL));
      String result = doPost(new URL(urlString), props,
         userAgent == null ? null : userAgent.toString(),
         redirects == null ? -1 : Integer.parseInt(redirects.toString()));
      System.out.println(result);
   }

   /**
    * Do an HTTP POST.
    * @param url the URL to post to
    * @param nameValuePairs the query parameters
    * @param userAgent the user agent to use, or null for the default user agent
    * @param redirects the number of redirects to follow manually, or -1 for automatic
    * redirects
    * @return the data returned from the server
    */
   public static String doPost(URL url, Map<Object, Object> nameValuePairs, String userAgent,
         int redirects) throws IOException
   {
      var connection = (HttpURLConnection) url.openConnection();
      if (userAgent != null)
         connection.setRequestProperty("User-Agent", userAgent);
```
