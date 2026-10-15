The code to respond to the asynchronous completion of a WCF service call looks like this:

```
void client_GetSomeStringCompleted(object sender,
    RegularServiceReference.GetSomeStringCompletedEventArgs e)
{
    Debug.WriteLine("Received reply from service:\n" + e.Result);
}
```

Although the return value and input parameters for this service call were simple strings, you can send and receive almost arbitrarily complex C# objects. So long as WCF knows how to serialize and deserialize the class, it will be able to generate a client-side proxy or client wrapper that does the busywork of going between raw HTTP payload and the client wrapper objects.

You can also invoke methods on a remote WCF service without adding a service reference and without using a generated proxy. This is done using a WCF class called a ChannelFactory, but that class and topics related to it are better handled by books written specifically about WCF. For more information about WCF, check out the book *Programming WCF Services* by Juval Lowy.

# Summary

Mobile applications rarely exist in a vacuum. Although there are some very popular and notable exceptions, in most cases mobile applications need to make use of network resources somehow. Whether this is to download the latest weather information, stock quotes, or to communicate with a proprietary hosted database, mobile applications are often nothing without their network resources.

This chapter provided you with an overview of how to build network-connected Windows Phone 7 applications. Whether you are using the WebClient or HttpWebRequest classes to communicate with RESTful services, or using generated WCF client proxies, exchanging data with network resources is simple, easy, and efficient. With networking capabilities now in your WP7 toolbox, you are ready to create amazing applications that users will enjoy and continue to use again and again.