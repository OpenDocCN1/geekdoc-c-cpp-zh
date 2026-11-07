+   6. In five seconds, the timer will trigger in CSECLNT, causing `CMainView::OnTimer()` to get called. No bytes are waiting to be sent yet, so the outgoing buffer is filled and written to the connected server.
+   7. `CMainView::OnStream()` is called in CSECLNT with a `CWINSOCK_DONE_WRITING` notice. The outgoing buffer is then marked as unused so that it may be used with the next triggering of `CMainView::OnTimer()`.
+   8. `CMainView::OnStream()` is called in CSECLNT with a `CWINSOCK_DONE_READING` notice. The data is read and immediately echoed back to the client.
+   9. `CMainView::OnStream()` is called in CSESRV with a `CWINSOCK_DONE_WRITING` notice. The data is then freed.
+   10. `CMainView::OnStream()` is called in CSECLNT with a `CWINSOCK_DONE_READING` notice. The echo data is read and then freed.
+   11. Another timer goes off in CSECLNT and the process repeats.

If CSECLNT is closed first, `CMainView::OnStream()` is called in CSESRV with a `CWINSOCK_LOST_CONNECTION` notice. If CSESRV is closed first, `CMainView::OnStream()` is called in CSECLNT with a `CWINSOCK_LOST_CONNECTION` notice.

# Summary

This chapter demonstrates the use of the `CWinSock`, `CDatagramSocket`, and `CStreamSocket` objects. These objects are designed to make socket programming easier for you.

It is hoped that the comparison of these sample programs with those of Chapter 8 proves that the design goals of the WinSock class library, described in Chapter 9, are met. A comparison also reveals one of the limitations of the `CDatagramSocket` and `CStreamSocket` objects. These objects don’t have the capability of letting the WinSock subsystem assign an unused port to a server socket. Instead, the port must be specified in terms of its port number or service name, in this case to port number 2000.

The next chapter uses the WinSock class library objects in a sample client-server database environment.