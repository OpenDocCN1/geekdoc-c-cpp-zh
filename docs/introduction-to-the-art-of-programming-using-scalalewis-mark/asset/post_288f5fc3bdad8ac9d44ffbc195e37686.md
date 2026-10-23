
so that outside entities can not get to it. Programs that run critical systems need to take precautions to make sure that they can not be taken down by individuals without the authorization to do so.

The chat program we just wrote failed on all counts in regards to security. Adding the proper error handling would be a major step in the direction to make sure that only the person running the server can take it down. However, every message coming in to and out of the server is sent pretty much as plain text that could be easily read at any number of points between the client and the server if sent across a network. Granted, this was not intended to be a highly secure system. It does nothing to even verify who is connecting to it. This does not mean that it would never be used to discuss things that people might want to keep private. Someone might feel that if they set up the server on a machine just temporarily, then no one they did not invite would have a chance to come in and snoop on what is being said. The problem with this assumption is that another party could be watching communication without even knowing about the server.

The standard way to circumvent someone from listening to network communications is to encrypt messages. The person could still see the message going by, but because it is encrypted they can not read it. The simplest way to do this with socket communication in Scala is to use a javax.net.ssl.SSLServerSocket on the server and connect with javax.net.ssl.SSLSockets. These make sockets that encrypt all communications using the Secure Socket Layer (SSL) protocol. This is the same protocol used by ssh and scp.

## 23.3 URLs

As was mentioned at the beginning of the chapter, you have likely been using networked programs for years. Most notable of these would be your web browser. Web browsers were originally written as little more than a program to pull information down from servers and display that information on your screen. Many web applications now have some 2-way communication, but there is still a lot on the web that can be accessed by simply pulling down information.

When you use a web browser to access information you have to tell it where you want to pull the information from and what information you want to pull down. This is done with a Uniform Resource Locator or URL. Most of the URLs you enter into a browser begin with "http". This tells the browser that it is supposed to communicate with the server using the Hypertext Transfer Protocol (HTTP). This is a standard for requesting information across sockets using fairly simple text commands. By default, HTTP servers sit on port 80 though other port numbers can be specified as part of the URL. You could pull down information from an HTTP server by opening a socket and sending the appropriate commands. However, because HTTP is so ubiquitous, there is a java.net.URL class that will help to do this for you.

There are a number of ways to build a URL where you can specify different parts of the URL, but the simplest to describe just takes a String with the same text that you would enter into a browser giving a complete specification of what information you want. For example, you could use the following line of code to get a URL for the main page of Scala.

```
import java.net._
val scalaURL = new URL("http://www.scala-lang.org/")
```

The URL class has a method called openStream that will return an InputStream that can be used to read the contents of the URL. We could use this in code like the following to read the complete contents of that URL and convert it to a String.

```
import java.io._
import collection.mutable
val urlis = new BufferedInputStream(scalaURL.openStream())
val buffer = mutable.Buffer[Byte]()
var res = urlis.read()
while(res>=0) {
  buffer += res.toByte
  res = urlis.read()
}
val contents = new String(buffer.toArray)
```

This code opens the stream and wraps it in a BufferedInputStream to improve performance. It then creates a Buffer[Byte] to hold the values that are read, then enters a loop where bytes are read one at a time and added to the buffer. This process ends when the value read is less than zero, indicating that the end of the stream has been reached. After the end has been reached, the buffer is converted to an array and a new String is built from that array.

The use of a while loop here is called for because we do not know how much data we are loading in advance and other approaches would require that. Instead of a while loop this could easily be converted to use a recursive function as well. Just make sure to specify @tailrec so that you know what you write will not overflow the stack. Knowing the length of the content would allow this alternate version, which is significantly simpler. The challenge is knowing what goes in place of the question marks.

```
import java.io._
val urlis = new BufferedInputStream(scalaURL.openStream())
val buffer = new Array[Byte](???) // Needs the size of the contents in bytes.
urlis.read(buffer)
val contents = new String(buffer)
```

It is tempting to call available on the stream. Unfortunately, this is not a good solution. That method returns the number of bytes that can be read before blocking. That number is often different from the total size. If the stream was just opened it will be small. Waiting for the full contents to become available is not an appropriate solution.

One way to do this that will work from some content is using a java.net.URLConnection. The URL class has a method called openConnection:URLConnection that can return one of these objects. The URLConnection has a getContentLength:Int method that will tell you the size of the contents of that URL. There is also a getContentLengthLong:Long method that can give you the size for content that exceeds the maximum size of an Int. A call to getInputStream:InputStream on the URLConnection will provide an input stream that you can read from.

```
import java.io._
val connection = scalaURL.openConnection()
val urlis = new BufferedInputStream(connection.getInputStream())
val buffer = new Array[Byte](connection.getContentLength)
urlis.read(buffer)
val contents = new String(buffer)
```

Unfortunately, the getContentLength method does not work with all types of content. If the length is not available, a value of -1 is returned which will cause this code to crash. For this reason, the while loop is probably the most robust solution.

If the URL pointed to something other than a text file, the data that was read would have to be handled in a different way. For example, it might point to an image. The URLConnection has a method called getContentType:String that can help you determine what type of data the URL references. You would then have to write code to load in the data and process it appropriately. There is also a method called getContent:AnyRef that is part of both URL and URLConnection. This method can return various things depending on the type of the contents. For example, getContent will return an image object if that is what the URL refers to. The fact that it returns AnyRef means that you should do a match on the value and handle it appropriately depending on what it is. The code might look something like this.

```
url.getContent() match {
  case img:java.awt.Image =>
    // Code for handling an image.
  case is:InputStream =>
    // This is what you get for text so you need code to read it.
  case _ =>
    // Some other type.
}
```

## 23.4 Remote Method Invocation (RMI)

In the next section we will be adding networking to the project in a way that will let users collaborate on a drawing while working on different programs. In order for this to work, they need to be able to share a drawing, chat with one another, and modify elements of that shared drawing. We could also consider adding other features to the sharing such as a sketch pad where they can doodle ideas. Now picture the code to implement these features using sockets.

The challenge that such an implementation will face is that there are many different types of messages being sent between the two users and those different messages can have an impact on very different parts of the code on either end. The code to handle this type of situation using sockets gets very messy. It might be tempting to use a different port for each type of message and keep many different sockets open, but such a solution is sloppy and does not scale. The operating system puts limits on the number of resources a single application can use. Instead, you have to send additional information with each message that identifies what type of message it is, and what objects it should be directed toward.

Dealing with that extra bookkeeping is challenging and time consuming to code. It is also difficult to debug. For these reasons, and the fact that this is something that happens in many applications, the Java libraries provide a simplified alternative called Remote Method Invocation (RMI). As the name implies, RMI lets you make method calls on objects that are located on other machines. It automatically handles the bookkeeping so that information is sent to the right place and the correct code is invoked on the opposite side. The downsides of RMI are that it does have a bit of a learning/setup curve, it only works between languages
