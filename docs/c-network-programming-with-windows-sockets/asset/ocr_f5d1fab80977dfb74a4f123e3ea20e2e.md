To send data, the application must provide the number of bytes to send and a pointer to the data. The data must remain allocated until the message handler discussed previously receives a message with `wParam` set to `CWINSOCK_DONE_WRITING` or `CWINSOCK_ERROR_WRITING`. In this case, `lParam` is the pointer initially passed to `Write()`. The data may also be unallocated if `Write()` returns an error value. The following code shows how `Write()` is called:

```
int nLen;
LPVOID pData;
int nStatus;

... allocate data buffer ...

nStatus = m_ps->Write(nLen, pData);
```

You have an option with the way the data buffer is allocated. You may allocate one buffer that gets continually reused. You know that it’s safe to reuse the buffer when the write notification message comes in with `wParam` set to `CWINSOCK_DONE_WRITING` or `CWINSOCK_ERROR_WRITING`. The other option you have is to allocate a new buffer whenever you want to send. In this case you would simply free each buffer when the `CWINSOCK_DONE_WRITING` or `CWINSOCK_ERROR_WRITING` message arrives.

To receive data, the application must provide a pointer to an integer to retrieve the number of bytes read. The `Read()` function returns a pointer to the data or `NULL` on error. `Read()` should be called when the message handler is activated with `wParam` set to `CWINSOCK_DONE_READING`. Following are the two ways to call `Read()`:

```
LPVOID pDataRead;
int nLen;

pDataRead = m_ps->Read(&nLen);
```

It’s the application’s responsibility to free the pointer returned by `Read()`.

To end the use of the stream socket object, call `DestroySocket()`, as in:

```
int nStatus;
nStatus = m_ps->DestroySocket();
```

# Summary

This chapter describes a class to manipulate a stream socket. The goal of this object is to enable the rapid development of a networked application using stream communication. The next chapter wraps up the class library. Chapters 14 through 16 use the `CStreamSocket` object in fully functional programs.