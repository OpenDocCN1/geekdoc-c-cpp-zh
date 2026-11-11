**java.net.InetSocketAddress** 1.4

- `InetSocketAddress(String hostname, int port)`
  constructs an address object with the given host and port, resolving the host name during construction. If the host name cannot be resolved, the address object's unresolved property is set to true.
- `boolean isUnresolved()`
  returns true if this address object could not be resolved.

**java.nio.channels.SocketChannel** 1.4

- `static SocketChannel open(SocketAddress address)`
  opens a socket channel and connects it to a remote address.

**java.nio.channels.Channels** 1.4

- `static InputStream newInputStream(ReadableByteChannel channel)`
  constructs an input stream that reads from the given channel.
- `static OutputStream newOutputStream(WritableByteChannel channel)`
  constructs an output stream that writes to the given channel.

# ### 4.3 Getting Web Data

To access web servers in a Java program, you will want to work at a higher level than socket connections and HTTP requests. In the following sections, we discuss the classes that the Java library provides for this purpose.

# #### 4.3.1 URLs and URLs

The URL and URLConnection classes encapsulate much of the complexity of retrieving information from a remote site. You can construct a URL object from a string:

```
var url = new URL(urlString);
```

If you simply want to fetch the contents of the resource, use the openStream method of the URL class. This method yields an InputStream object. Use it in the usual way—for example, to construct a Scanner:

```
InputStream inStream = url.openStream();
var in = new Scanner(inStream, StandardCharsets.UTF_8);
```