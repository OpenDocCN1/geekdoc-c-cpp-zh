
But here is the important part: While the hardware device is performing the I/O operation, your thread that issued the I/O request has nothing to do, so Windows puts your thread to sleep so that it is not wasting CPU time (#6). This is great, but while your thread is not wasting time, it is wasting space (memory), as its user-mode stack, kernel-mode stack, thread environment block (TEB), and other data structures are sitting in memory but are not being accessed at all. This is bad.

Ultimately, the hardware device will complete the I/O operation, and then Windows will wake up your thread, schedule it to a CPU, and let it return from kernel mode to user mode, and then back to managed code (#7, #8, and #9). **FileStream’s Read** method now returns an **Int32**, indicating the actual number of bytes read from the file so that you know how many bytes you can examine in the **Byte[]** that you passed to **Read**.

Let’s imagine that you are implementing a Web application and as each client request comes in to your server, you need to make a database request. When a client request comes in, a thread pool thread will call into your code. If you now issue a database request synchronously, the thread will block for an indefinite amount of time waiting for the database to respond with the result. If during this time another client request comes in, the thread pool will have to create another thread and again this thread will block when it makes another database request. As more and more client requests come in, more and more threads are created, and all these threads block waiting for the database to respond. The result is that your Web server is allocating lots of system resources (threads and their memory) that are barely even used!

And to make matters worse, when the database does reply with the various results, threads become unblocked and they all start executing. But since you might have lots of threads running and relatively few CPU cores, Windows has to perform frequent context switches, which hurts performance even more. This is no way to implement a scalable application.

Now, let’s discuss how Windows performs asynchronous I/O operations. In Figure 27-2, I have removed all the hardware devices except the hard disk from the picture, I introduce the common language runtime’s (CLR’s) thread pool, and I’ve modified the code slightly. I still open the disk file by constructing a **FileStream** object, but now I pass in the **FileOptions.Asynchronous** flag. This flag tells Windows that we may read and write operations against the file to be performed asynchronously.

![](img/3c46ff5b170881db4209d365b1f7a808_775_0.png)

**FIGURE 27-2** How Windows performs an asynchronous I/O operation

To read data from the file, I now call **BeginRead** instead of **Read**. Like **Read**, **BeginRead** calls Win32’s **ReadFile** function (#1). **ReadFile** allocates its IRP, initializes it just like it did in the synchronous scenario (#2), and then passes it down to the Windows kernel (#3). Windows adds the IRP to the hard disk driver’s IRP queue (#4), but now, instead of blocking your thread, your thread is allowed to return to your code; your thread immediately returns from its call to **BeginRead** (#5, #6, and #7). Now, of course, the IRP has not necessarily been processed yet, so you cannot have code after **BeginRead** that attempts to access the bytes in the passed-in **Byte[]**.

Now you might ask, when and how do you process the data that will ultimately be read? Well, when you call **BeginRead**, you pass it the name of a callback method as an argument (**CallBackMethod** in my example). The delegate referring to your callback method is effectively passed inside the IRP all the way down to the device driver. When the hardware device completes processing the IRP (a), it will queue the IRP’s delegate into the CLR’s thread pool (b). Sometime in the future, a thread pool thread will extract the completed IRP and invoke your callback method (c).¹ So now you know when the operation has completed, and inside this method, you can safely access the data inside the **Byte[]**.

1 Completed IRPs are extracted from the thread pool using a first-in first-out (FIFO) algorithm.

## The CLR’s Asynchronous Programming Model (APM)

Performing asynchronous operations is the key to building high-performance, scalable applications that allow you to use very few threads to execute a lot of operations. And when coupled with the thread pool, asynchronous operations allow you to take advantage of all of the CPUs that are in the machine. Realizing the enormous potential here, Microsoft’s CLR team designed a pattern that would make it easy for developers to take advantage of this capability. This pattern is called the Asynchronous Programming Model (APM).

Personally, I love the APM because it is relatively easy to learn, simple to use, and is supported by many types in the FCL. Here are some examples:

- All System.IO.Stream-derived classes that communicate with hardware devices (including FileStream and NetworkStream) offer BeginRead and BeginWrite methods. Note that Stream-derived classes that do not communicate with hardware devices (including BufferedStream, MemoryStream, and CryptoStream) also offer BeginRead and BeginWrite methods to fit into the APM. However, the code in these methods performs compute-bound operations, not I/O-bound operations, and therefore a thread is required to execute these operations.
- The System.Net.Dns class offers BeginGetHostAddresses, BeginGetHostByName, BeginGetHostEntry, and BeginResolve methods.
- The System.Net.Sockets.Socket class offers BeginAccept, BeginConnect, BeginDisconnect, BeginReceive, BeginReceiveFrom, BeginReceiveMessageFrom, BeginSend, BeginSendFile, and BeginSendTo methods.
- All System.Net.WebRequest-derived classes (including FileWebRequest, FtpWebRequest, and HttpWebRequest) offer BeginGetRequestStream and BeginGetResponse methods.
- The System.IO.Ports.SerialPort class has a read-only BaseStream property that returns a Stream, which, as you know, offers BeginRead and BeginWrite methods.
- The System.Data.SqlClient.SqlCommand class offers BeginExecuteNonQuery, BeginExecuteReader, and BeginExecuteXmlReader methods.

Furthermore, all delegate types define a BeginInvoke method for use with the APM. And finally, tools (such as WSDL.exe and SvcUtil.exe) that produce Web service proxy types also generate BeginXxx methods for use with the APM. By the way, there is a corresponding EndXxx method for each and every BeginXxx method. As you can see, support for the APM is pervasive throughout the FCL.

To synchronously read bytes from a FileStream, you’d call its Read method, which is prototyped as follows:

```
public Int32 Read(Byte[] array, Int32 offset, Int32 count)
```

Calling a function that internally performs synchronous I/O puts your application in an unpredictable state as you have no idea when (or even if) the method will return. What if the file you opened was on a network server and just before calling `Read`, the server lost power? Now when will `Read` return?

And so, if you are interested in writing responsive, robust, and scalable software, you should not call methods that perform synchronous I/O; you should instead call methods that perform asynchronous I/O. To asynchronously perform an I/O operation, you would call a `BeginXxx` method like `FileStream`'s `BeginRead` method:

```
IAsyncResult BeginRead(Byte[] array, Int32 offset, Int32 numBytes,
    AsyncCallback userCallback, Object stateObject)
```

Notice that `BeginRead`'s first three parameters are identical to those of `Read`. And, in fact, every `BeginXxx` method has the same parameters as its synchronous counterpart method. But, every `BeginXxx` method has two additional parameters: `userCallback` and `stateObject`. The `userCallback` parameter is of the `AsyncCallback` delegate type:

```
public delegate void AsyncCallback(IAsyncResult ar);
```

For this parameter, you pass the name of a method (or lambda expression) representing code that you want to be executed by a thread pool thread when the asynchronous I/O operation completes. The last parameter to a `BeginXxx` method, `stateObject`, is a reference to any object you'd like forwarded on to your callback method. Inside your callback method, you access your `objectState` by querying the `IAsyncResult` interface's read-only `AsyncState` property.

All `BeginXxx` methods return an object that implements the `System.IAsyncResult` interface. When you call a `BeginXxx` method, it constructs an object that uniquely identifies your I/O request, queues up the request to the Windows device driver, and returns to you a reference to the `IAsyncResult` object. You can think of this object as your receipt. You can actually ignore the object reference returned from `BeginXxx` because the CLR internally holds a reference to the `IAsyncResult` object as well. When the operation completes, a thread pool thread will invoke your callback method, passing to it a reference to the internally held `IAsyncResult` object.

Inside your method, you'll call the corresponding `EndXxx` method, passing it the `IAsyncResult` object. The `EndXxx` method returns the same result that you would have gotten if you had called the synchronous method. For example, `FileStream`'s `Read` method returns an `Int32` that indicates the number of bytes actually read from the stream. `FileStream`'s `EndRead` method's return value has the same meaning:

```
Int32 EndRead(IAsyncResult result);  // Returns number of bytes read from the stream
```

Below is the code for a named-pipe server class, `PipeServer`, which is implemented using the APM:
