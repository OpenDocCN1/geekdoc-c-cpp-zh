datagram echo server is made. If the attempt succeeds and bytes are written, the number of bytes to send is reset to 0 (zero). If there was an error sending but the error was simply that the send would block, the count of bytes to send is retained because you’ll get a real FD_WRITE eventually.

Assuming that DECLIENT sends a buffer, CMainView::OnAsyncSelect() is called in DESERV with an FD_READ notice. If the data is read successfully, a byte count is recorded, the originator of the data is noted, and a fake FD_WRITE message is generated to force the sending of the just-received data back to the originator (DECLIENT).

CMainView::OnAsyncSelect() is called in DESERV with an FD_WRITE event. There are bytes to be sent, so an attempt to transmit them to the datagram echo client is made. If the attempt succeeds and bytes are written, the number of bytes to send is reset to 0 (zero). If there was an error sending but the error was simply that the send would block, the count of bytes to send is retained because you’ll get a real FD_WRITE eventually.

Assuming that DESERV sends a buffer, CMainView::OnAsyncSelect() is called in DECLIENT with an FD_READ notice and the client reads the echoed data.

Another timer goes off in DECLIENT and the process repeats.

Figure 8.9 shows DESERV and DECLIENT running on the same computer, which has the IP address 166.78.16.150. The server and client were assigned ports 1059 and 1060, respectively. Notice that after each application initialized, it received an FD_WRITE notification. WinSock is simply telling the application that the socket is in a writeable state. The applications ignore the message unless they have bytes to send.

# **FIGURE 8.9.**

DESERV and
DECLIENT running
on the same computer.

![](bbox=[0.401, 0.628, 0.856, 0.902])