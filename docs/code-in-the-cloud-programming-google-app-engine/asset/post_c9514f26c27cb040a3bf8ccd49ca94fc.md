
## 9.3 RPC in GWT

Now we get to the complicated part.

As I mentioned before, AJAX code is not written explicitly in GWT. Instead, we write something called a *remote procedure call* (RPC). An RPC is something that looks almost like a normal method call, but under the covers, it's translated by the system into a request sent from the client to the server. The return value of the RPC is the response sent from the server back to the client.

Just like any other RPC system, there's a client side and a server side in GWT. We can look at the code for them separately; it's up to the GWT RPC system to string them together.

If you've done any distributed programming, Google-style RPC is probably not what you're used to. Traditionally, RPC tries to appear as much like a traditional function call as possible. In other words, if we want to provide an RPC for a factorial function, the function implementation would look like a traditional function declaration, and an invocation of it would look like a traditional invocation. For example, Java has a native RPC layer, where we define a remote object by an interface, and then we can invoke methods on an object of the interface type.

We could define a factorial service as a Java interface:

```java
public interface Fact extends Remote {
    int fact(int n);
}
```

Then in code that uses it, we'd acquire a handle for the remote interface and invoke it directly with something like this:

```java
int j = f.fact(n);
```

Wrapped around that, we'd have some plumbing in the server to make the object available so that the client can get a handle for it, and we would likewise have code on the client to get hold of a handle on the remote object. But the invocation itself looks like a normal, local invocation.

There's a problem with this approach: communication is slow. A remote procedure call can easily take two orders of magnitude more time than a local call. In a traditional call, the code is stuck waiting until it gets the response back from the server. That's a huge waste of time, and it can create unacceptable delays in our user interface.

Google therefore uses something called *asynchronous* or *continuation passing* style for remote calls. The call itself returns nothing. Instead, it takes an extra parameter, which is a function to invoke on the result of the RPC whenever it’s received.

For example, imagine we have a factorial service. In traditional style, what we want to do is this:

```java
System.out.println("Foo = " + Math.log(3 * f.fact(n)));
```

In continuation passing style, that would be something like this:

```java
f.fact(n, new AsyncCallback<Integer>() {
    public void onSuccess(Integer result) {
        System.out.println("Foo = " + Math.log(3 * result));
    }
});
```

All I did was take the original code that was going to use the return value of the RPC and wrap it up in an object that I could pass to the remote call. All that does is start the process. My code can go off and do other things while the RPC is translating the call to a message, sending it, waiting for the server to send a response, and then translating the response message back to a result value. Whenever the result comes back, the callback will be invoked, and the result of the call will be processed.

It can feel a bit unnatural when you’re used to imperative programming. (Functional programmers do this all the time, even when they’re not doing distributed programming.) It takes some time to get used to, and even then, it sometimes seems a bit twisted. But overall, the advantage of not having to wait for the RPC outweighs the problems. It makes applications more responsive to the users, and that’s the most important thing.

### Client-Side RPC in GWT

No matter how great a toolkit is, communication is never simple. We need to be able to deal with translating parameters into a format that can be passed as a message, and we need to be able to deal with delays or even failures due to the network. To cope with that, GWT uses a very Google-ish idiom. At Google, we have some very distinctive and stylized ways of handling certain basic problems. In particular, we have a way of doing remote procedure calls using an asynchronous response handler. It’s pretty foreign to people who haven’t done a lot of distributed programming in the Google style. In general, GWT is really terrific about making plumbing invisible. However, in this case they decided not to.

- 3. This is the synchronous method declaration. Any parameters to a service method must extend either `java.io.Serializable` or the GWT specific variant `com.google.gwt.user.client.rpc.IsSerializable`. One thing that’s very important to understand here is that GWT using the Java serialization interface to mark classes that will be passed in an RPC does *not* mean that it uses Java serialization. The use of either IsSerializable or Serializable is just a marker to tell GWT that it needs to generate code to serialize and deserialize the type. The actual format that GWT uses is not even close to compatible with Java’s standard serialization.

  The method declaration itself is completely standard: it’s just a normal interface method declaration.

In addition to the synchronous interface, we also need to write an asynchronous interface. This is one of the places where I’m frankly mystified why the GWT team didn’t provide some automatic support. To generate the asynchronous interface, we just write another interface, which is a pure boilerplate translation of the synchronous interface. It must have methods with exactly the same name as the methods in the synchronous interface; each method must have return type void; and each method adds a parameter at the end, which is an AsyncCallback and whose type parameter is the return type of the synchronous method. For example:

Download workspace/HelloChat/src/com/pragprog/ebook/hellochat/client/GreetingServiceAsync.java

```java
package com.pragprog.ebook.hellochat.client;

import com.google.gwt.user.client.rpc.AsyncCallback;

/**
 * The async counterpart of <code>GreetingService</code>.
 */
public interface GreetingServiceAsync {
    void greetServer(String input, AsyncCallback<String> callback);
}
```

The asynchronous interface doesn’t have any explicit connection to the synchronous interface, and it doesn’t have to use any special annotations or inherit from any special class. It’s really only used by the client—the actual plumbing to map between the asynchronous and synchronous interfaces is generated by GWT. The only purpose of the asynchronous interface is to provide the call interface that the client will use.

### Server-Side RPC in GWT

The server side of GWT RPC is amazingly simple. We just implement the synchronous client interface using a class that extends RemoteServiceServlet. For our greeting service, that implementation is as follows:

Download workspace/HelloChat/src/com/pragprog/ebook/hellochat/server/GreetingServiceImpl.java

```java
package com.pragprog.ebook.hellochat.server;
import com.pragprog.ebook.hellochat.client.GreetingService;
import com.google.gwt.user.server.rpc.RemoteServiceServlet;

/**
 * The server-side implementation of the RPC service.
 */
@SuppressWarnings("serial")
public class GreetingServiceImpl extends RemoteServiceServlet implements
        GreetingService {

    public String greetServer(String input) {
        String serverInfo = getServletContext().getServerInfo();
        String userAgent = getThreadLocalRequest().getHeader("User-Agent");
        return "Hello, " + input + "!<br><br>I'm running " +
                serverInfo + "<br><br>It looks like you are using:<br>" +
                userAgent;
    }
}
```

The @SuppressWarnings annotation is a little unusual. It’s there because serialization in later generations of the Java virtual machine uses a version identifier for each class file. If we have a class that implements `java.io.Serializable`, Java generates a warning if we don’t provide it with a version identifier field. Service implementations always implement Serializable, because RemoteServiceServlet inherits from the standard servlet class, which implements Serializable. Since GWT doesn’t use the version identifier, including it in the code would just be pointless clutter; the annotation prevents the compiler from generating a confusing warning message.

And that’s all we need to do on the server side. Of course, it gets more complex when we want to do persistence using datastore. But we’ll save that for the next chapter.

So now we’ve got the full RPC for our hello application in place. It’s a lot cleaner than the way we did AJAX back in Python: we have a well-defined interface, and we can invoke it just by making a method call. We don’t need to worry about creating XmlHTTPRequests, parsing parameters, checking status codes, or any of the messy and error-prone things we needed to do in Python.
