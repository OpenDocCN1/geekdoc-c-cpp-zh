# **FIGURE 15.2.**

*The server INISRV.*

![](bbox=[0.423, 0.13, 0.835, 0.412])

There is much room for improvement in the client and server programs, though. One important enhancement might be the ability to handle database commands and responses that do not arrive in one contiguous block. Presently, the client and server can't handle such a circumstance. Luckily, however, the blocks of data being transferred are relatively small and hence have little fragmentation on a lightly loaded network. This enhancement would entail modifying the C WINSOCK_DONE_READING handlers for the stream socket objects to buffer the incoming bytes until an entire DBCOMMAND structure arrives.

The next chapter uses the WinSock class library object in a finger application for a heterogeneous UNIX environment.