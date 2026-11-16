
## 28.1 History of Remote Procedure Call

The idea of the remote procedure call goes back to 1976, when it was described in RFC 707 [1] as an inter-process communication (IPC) technology. An IPC is a set of techniques for the exchange of data among multiple threads in one or more processes that may be running on one or more computers connected by a network. IPC techniques are divided into methods for message passing, synchronization, shared memory, and remote procedure calls. One of the first business uses of RPC was by Xerox under the name "Courier" in 1981 [2].

The first popular implementation of RPC was Sun's RPC, now called ONC RPC. It is still widely used today on several platforms [3, 4]. Another early implementation was Apollo Computer's NCS (Network Computing System). It was used as the foundation of DCE/RPC. A decade later (in the mid 1990s), Microsoft adopted DCE/RPC as the basis of Microsoft RPC (MSRPC), and implemented DCOM atop it.

## 28.2 How RPC Works: Internal Architecture of RPC

An RPC is initiated by the client sending a request message to a known remote server in order to execute a specified procedure using supplied parameters. A response is returned to the client where the application continues along with its process. While the server is processing the call, the client is blocked—it waits until the server has finished processing before resuming execution.

Figure 28.2 shows the flow of activity that takes place during an RPC call between two networked systems. Like a function call, when an RPC is made, the calling arguments are passed to the remote procedure, and the caller waits for a response to be returned from the remote procedure. The steps are the following:

- 1. The client makes a procedure call that sends a request to the server and waits. The thread is blocked from processing until either a reply is received or the RPC times out.
- 2. When the request arrives, the server calls a dispatch routine that prepares the requested service.
- 3. The requested service is performed on the server.
- 4. The server sends the result to the client.
- 5. After the RPC is completed, the client program continues.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_546_0.png)

**Figure 28.2:** Steps during an RPC call, initiated by the client sending a request to the server.

An important difference between remote procedure calls and local calls is that remote calls can fail because of unpredictable network problems. Also, callers generally must deal with such failures without knowing whether the remote procedure was actually invoked.

Note that in this remote procedure call model, only one of the two processes is active at any given time. However, this scenario is given only as an example. The RPC protocol makes no restrictions on concurrency, and other scenarios are possible. For example, an implementation may choose to have asynchronous RPC calls so the client may do useful work while waiting for the reply from the server. Another possibility is to have the server create a separate task to process an incoming request so the server can be free to receive other requests.

Code that calls remotely makes use of a low-level subsystem. The encoding and decoding of procedure calls is handled in a special stub module (see Figure 28.3). That RPC stub module handles the procedure identification and the marshalling of the supplied procedure parameters inside a message that has to be sent or has been received. The RPC protocol is independent of transport protocols; that is, RPC does not care how a message is passed from one process to another — the protocol is concerned only with the specification and interpretation of messages. For example, RPC may be implemented on top of TCP/IP or UDP/IP. Also, the act of binding a client to a server is not part of the RPC subsystem. This function is left to some higher-level software module.

![](img/7ba1225bb0e5a87be0fd35866408ffa7_547_0.png)

**Figure 28.3:** Encoding and decoding of procedure calls in special stub modules.

A remote procedure is uniquely identified by the following three pieces of information:

- 1. The program number.
- 2. The version number.
- 3. The procedure number.

The program number A identifies a group of related remote procedures, each of which has a unique procedure number. A program may consist of one or more versions, and each version consists of a collection of procedures that are available to be called remotely. The version number B enables multiple versions of an RPC protocol to be available simultaneously. Each version contains a number of procedures that can be called remotely, and each procedure has a procedure number C.

## 28.3 How to Build Your Own RPC Subsystem

We have seen that the RPC technology must allow a computer program to cause a procedure to execute in another address space (commonly on another computer on a shared network) without the programmer explicitly coding the details for this remote interaction. That means that the RPC stub modules have to handle a number of tasks. On the client side, the stub has to hide the fact that the called procedure is going to run in a different process (on the same machine or on a different machine). On the server side, the stub has to hide that the procedure call was initiated in a different (client) process and that the result is going to be sent back. These tasks the stubs have to handle lead to a list of points that should be kept in mind when you start to implement your own RPC subsystem.

The remote procedure call mechanism must behave similarly to that of the local procedure call model. With the local model, the caller places arguments to a procedure in a well-specified location (such as in particular registers or on the stack) and transfers control to the procedure. When the caller eventually regains control, it extracts the result of the procedure from the well-specified location and continues execution.

With respect to the remote procedure call paradigm, a client calls the stub version of the wanted procedure to initiate the processing of the wanted calculations. Now, the called function in the client RPC stub module has to encode all needed information in a data packet to be able to force the remote processing of the wanted procedure by sending this packet to a server. This means that the procedure identification and all function parameters have to be encoded in this data packet. On the server side, a process is waiting for the arrival of a client message. When a call message arrives, the server runs a dispatch routine in its RPC stub that extracts the procedure identification and its parameters, performs the requested procedure to compute the results, encodes these results in a new data packet, and sends it back to the client. Then the server waits for the arrival of the next call message. The resulting packet of the procedure call returns to the client where it has to be dispatched. Finally, the procedure that initiated the processing of the wanted calculations regains control, continues execution, and can handle the result (see Figure 28.4).

![](img/7ba1225bb0e5a87be0fd35866408ffa7_549_0.png)

**Figure 28.4:** RPC stub modules handling the procedure identification and the marshalling of the supplied procedure parameters.

We have already seen that the identification of the wanted remote procedure must be encoded in the client RPC stub in a set of three numbers: the program number A, the version number B, and the procedure number C. That information enables the receiving and decoding RPC stub module in the server application to identify the function that must be processed. Beside this procedure identification, the client/server stub modules have to handle the marshalling of the procedure parameters. There are three different solutions for passing the parameters:

- A parameter can be passed by value—this means a local value that can be modified.
- A parameter can be passed by reference—this means the parameter is a pointer to a value that must be handled via call-to-copy/restore.
- A parameter can be a pointer to a complex data structure such as a list, tree, etc. The server could read structure elements from the client one at a time, but this would be very inefficient. A better way is to copy the complete data structure to the server address space.

With respect to possible different representation of integer and float values, characters, and other data on client and server machines, you have to be able to handle system-specific issues, especially the mixing of little endian and big endian byte ordering. You have to encode information about the data format of the packed parameters, or you have to use a machine-independent transfer format for data.

The simple code fragments shown in Listing 28.1 should give you an idea of how to implement the stub functions for client and server machines.

**Listing 28.1:** Example stub functions for the client and server.

```
// IN THE CLIENT RPC STUB

// example of a client stub version of "procedureA"
// client application calls this local procedure to
// "procedureA" in the server application

int ClientRPCStub::procedureA(int parameter)
{
    // encode a data packet
    Pack outPacket(getProcID(this), getMshParams (para
```
