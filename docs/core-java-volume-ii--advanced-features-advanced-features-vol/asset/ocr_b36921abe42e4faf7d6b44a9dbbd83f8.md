# 4.3.2 Using a URLConnection to Retrieve Information

If you want additional information about a web resource, you should use the URLConnection class, which gives you much more control than the basic URL class.

When working with a URLConnection object, you must carefully schedule your steps.

+   1. Call the `openConnection` method of the URL class to obtain the URLConnection object:

```
URLConnection connection = url.openConnection();
```

+   2. Set any request properties, using the methods

```
setDoInput
setDoOutput
setIfModifiedSince
setUseCaches
setAllowUserInteraction
setRequestProperty
setConnectTimeout
setReadTimeout
```

We discuss these methods later in this section and in the API notes.

+   3. Connect to the remote resource by calling the connect method:

```
connection.connect();
```

Besides making a socket connection to the server, this method also queries the server for *header information*.

+   4. After connecting to the server, you can query the header information. Two methods, `getHeaderFieldKey` and `getHeaderField`, enumerate all fields of the header. The method `getHeaderFields` gets a standard Map object containing the header fields. For your convenience, the following methods query standard fields:

```
getContentType
getContentLength
getContentEncoding
getDate
getExpiration
getLastModified
```

+   5. Finally, you can access the resource data. Use the `getInputStream` method to obtain an input stream for reading the information. (This is the same input stream that the `openStream` method of the URL class returns.) The other method, `getContent`, isn’t very useful in practice. The objects that are returned by standard content types such as `text/plain` and `image/gif` require