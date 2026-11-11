
classes in the `com.sun` hierarchy for processing. You could register your own content handlers, but we do not discuss this technique in our book.

> **CAUTION:** Some programmers form a wrong mental image when using the `URLConnection` class, however. For that reason, it is important that you follow the setup steps for the connection.

Let us now look at some of the `URLConnection` methods in detail. Several methods set properties of the connection before connecting to the server. The most important ones are `setDoInput` and `setDoOutput`. By default, the connection yields an input stream for reading from the server but no output stream for writing. If you want an output stream (for example, for posting data to a web server), you need to call

```
connection.setDoOutput(true);
```

Next, you may want to set some of the request headers. The request headers are sent together with the request command to the server. Here is an example:

```
GET www.server.com/index.html HTTP/1.0
Referer: http://www.somewhere.com/links.html
Proxy-Connection: Keep-Alive
User-Agent: Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.8.1.4)
Host: www.server.com
Accept: text/html, image/gif, image/jpeg, image/png, */*
Accept-Language: en
Accept-Charset: iso-8859-1,utf-8
Cookie: orangemilano=19218887281987
```

The `setIfModifiedSince` method tells the connection that you are only interested in data modified since a certain date.

Finally, you can use the catch-all `setRequestProperty` method to set any name/value pair that is meaningful for the particular protocol. For the format of the HTTP request headers, see RFC 2616. Some of these parameters are not well documented and are passed around by word of mouth from one programmer to the next. For example, if you want to access a password-protected web page, you must do the following:

1. Concatenate the user name, a colon, and the password.

```
String input = username + ":" + password;
```

2. Compute the Base64 encoding of the resulting string. (The Base64 encoding encodes a sequence of bytes into a sequence of printable ASCII characters.)

```
Base64.Encoder encoder = Base64.getEncoder();
String encoding = encoder.encodeToString(input.getBytes(StandardCharsets.UTF_8));
```

3. Call the setRequestProperty method with a name of "Authorization" and the value "Basic " + encoding.

```
connection.setRequestProperty("Authorization", "Basic " + encoding);
```

> **TIP:** You just saw how to access a password-protected web page. To access a password-protected file by FTP, use an entirely different method: Construct a URL of the form
>
> ftp://username:password@ftp.yourserver.com/pub/file.txt

Once you call the connect method, you can query the response header information. First, let's see how to enumerate all response header fields. The implementors of this class felt a need to express their individuality by introducing yet another iteration protocol. The call

```
String key = connection.getHeaderFieldKey(n);
```

gets the nth key from the response header, where n starts from 1! It returns null if n is zero or greater than the total number of header fields. There is no method to return the number of fields; you simply keep calling getHeaderFieldKey until you get null. Similarly, the call

```
String value = connection.getHeaderField(n);
```

returns the nth value.

The method getHeaderFields returns a Map of response header fields.

```
Map<String,List<String>> headerFields = connection.getHeaderFields();
```

Here is a set of response header fields from a typical HTTP request:

```
Date: Wed, 27 Aug 2008 00:15:48 GMT
Server: Apache/2.2.2 (Unix)
Last-Modified: Sun, 22 Jun 2008 20:53:38 GMT
Accept-Ranges: bytes
Content-Length: 4613
Connection: close
Content-Type: text/html
```

> **NOTE:** You can obtain the response status line (such as "HTTP/1.1 200 OK") as `connection.getHeaderField(0)` or `headerFields.get(null)`.

As a convenience, six methods query the values of the most common header types and convert them to numeric types when appropriate. Table 4.1 shows these convenience methods. The methods with return type long return the number of seconds since January 1, 1970 GMT.

### Table 4.1 Convenience Methods for Response Header Values

| Key Name | Method Name | Return Type |
| --- | --- | --- |
| Date | `getDate` | `long` |
| Expires | `getExpiration` | `long` |
| Last-Modified | `getLastModified` | `long` |
| Content-Length | `getContentLength` | `int` |
| Content-Type | `getContentType` | `String` |
| Content-Encoding | `getContentEncoding` | `String` |

The program in Listing 4.6 lets you experiment with URL connections. Supply a URL and an optional user name and password on the command line when running the program, for example:

```
java urlConnection.URLConnectionTest http://www.yourserver.com user password
```

The program prints

- All keys and values of the header
- The return values of the six convenience methods in Table 4.1
- The first ten lines of the requested resource

### Listing 4.6 `urlConnection/URLConnectionTest.java`

```java
package urlConnection;

import java.io.*;
import java.net.*;
import java.nio.charset.*;
import java.util.*;

/**
 * This program connects to an URL and displays the response header data and the first
 * 10 lines of the requested data.
 *
 * Supply the URL and an optional username and password (for HTTP basic authentication) on the
 * command line.
 * @version 1.2 2018-03-17
 * @author Cay Horstmann
 */
public class URLConnectionTest
{
   public static void main(String[] args)
   {
      try
      {
         String urlName;
         if (args.length > 0) urlName = args[0];
         else urlName = "http://horstmann.com";

         var url = new URL(urlName);
         URLConnection connection = url.openConnection();

         // set username, password if specified on command line

         if (args.length > 2)
         {
            String username = args[1];
            String password = args[2];
            String input = username + ":" + password;
            Base64.Encoder encoder = Base64.getEncoder();
            String encoding = encoder.encodeToString(input.getBytes(StandardCharsets.UTF_8));
            connection.setRequestProperty("Authorization", "Basic " + encoding);
         }

         connection.connect();

         // print header fields

         Map<String, List<String>> headers = connection.getHeaderFields();
         for (Map.Entry<String, List<String>> entry : headers.entrySet())
         {
            String key = entry.getKey();
            for (String value : entry.getValue())
               System.out.println(key + ": " + value);
         }

         // print convenience functions

System.out.println("----------");
System.out.println("getContentType: " + connection.getContentType());
System.out.println("getContentLength: " + connection.getContentLength());
System.out.println("getContentEncoding: " + connection.getContentEncoding());
System.out.println("getDate: " + connection.getDate());
System.out.println("getExpiration: " + connection.getExpiration());
System.out.println("getLastModified: " + connection.getLastModified());
System.out.println("----------");

String encoding = connection.getContentEncoding();
if (encoding == null) encoding = "UTF-8";
try (var in = new Scanner(connection.getInputStream(), encoding))
{
    // print first ten lines of contents

    for (int n = 1; in.hasNextLine() && n <= 10; n++)
        System.out.println(in.nextLine());
    if (in.hasNextLine()) System.out.println(". . .");
}
catch (IOException e)
{
    e.printStackTrace();
}
      }
   }
}
```

| API | Description |
| --- | --- |
| `java.net.URL` (1.0) | |
| `InputStream openStream()` | opens an input stream for reading the resource data. |
| `URLConnection openConnection()` | returns a URLConnection object that manages the connection to the resource. |

| API | Description |
| --- | --- |
| `java.net.URLConnection` (1.0) | |
| `void setDoInput(boolean doInput)` | If doInput is true, the user can receive input from this URLConnection. |
| `boolean getDoInput()` | If doInput is true, the user can receive input from this URLConnection. |
| `void setDoOutput(boolean doOutput)` | If doOutput is true, the user can send output to this URLConnection. |
| `boolean getDoOutput()` | If doOutput is true, the user can send output to this URLConnection. |
