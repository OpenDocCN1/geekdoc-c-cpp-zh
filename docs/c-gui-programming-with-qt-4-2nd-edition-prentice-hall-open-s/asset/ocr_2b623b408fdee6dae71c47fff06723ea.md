```
setHost("www.trolltech.com");
http.request(header("qt-interest=on&search=opengl"));
```

**QHttp** emits the requestStarted(int) signal when it starts executing a request, and it emits the requestFinished(int, bool) signal when the request has finished. The int parameter is an ID number that identifies a request. If we are interested in the fate of individual requests, we can store the ID numbers when we schedule the requests. Keeping track of the ID numbers allows us to provide detailed feedback to the user.

In most applications, we only want to know whether the entire sequence of requests completed successfully or not. This is easily achieved by connecting to the done(bool) signal, which is emitted when the request queue becomes empty.

When an error occurs, the request queue is automatically cleared. But if we schedule new requests after the error has occurred using the same QHttp object, these requests will be queued and sent as usual.

Like QFtp, QHttp provides a readyRead() signal as well as the read() and readAll() functions that we can use instead of specifying an I/O device.