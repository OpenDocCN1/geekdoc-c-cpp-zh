+   **java.net.URLConnection 1.0** *(Continued)*
+   
+   - `String getHeaderFieldKey(int n)`
+     gets the key for the nth response header field, or null if n is ≤ 0 or greater than the number of response header fields.
+   - `String getHeaderField(int n)`
+     gets value of the nth response header field, or null if n is ≤ 0 or greater than the number of response header fields.
+   - `int getContentLength()`
+     gets the content length if available, or -1 if unknown.
+   - `String getContentType()`
+     gets the content type, such as text/plain or image/gif.
+   - `String getContentEncoding()`
+     gets the content encoding, such as gzip. This value is not commonly used, because the default identity encoding is not supposed to be specified with a Content-Encoding header.
+   - `long getDate()`
+   - `long getExpiration()`
+   - `long getLastModified()`
+     gets the date of creation, expiration, and last modification of the resource. The dates are specified as seconds since midnight, GMT, January 1, 1970.
+   - `InputStream getInputStream()`
+   - `OutputStream getOutputStream()`
+     returns a stream for reading from the resource or writing to the resource.
+   - `Object getContent()`
+     selects the appropriate content handler to read the resource data and convert it into an object. This method is not useful for reading standard types such as text/plain or image/gif unless you install your own content handler.

# ### 4.4.3 Posting Form Data

In the preceding section, you saw how to read data from a web server. Now we will show you how your programs can send data back to a web server and to programs that the web server invokes.

To send information from a web browser to the web server, a user fills out a *form*, like the one in Figure 4.8.