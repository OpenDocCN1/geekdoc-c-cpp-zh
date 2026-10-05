# 484 Chapter 6. Special Topic: Networks and Message Passing

tage is to hide the conversion of the port number from host to network format (most likely little endian to big endian format).

The system call listen() on line 13 marks the socket for listening with a backlog of 10. The system socketport will keep up to 10 clients waiting for a connection but no more. The system call listen() is nonblocking. It does not actually listen.

Lines 15 and 16 use setsockopt() to ensure that the port address can be safely reused after the server is shut down. This function returns the socket file descriptor socketport (line 17).

Many servers have firewalls that block incoming connections on all ports a chosen few. For this program to work, the firewall must be modified to accept connections on port 28537.

Once the socket has been bound to a port and marked for listening, it is ready to accept connections.

```
int connect2(int socketport){
    int socketclient;
    socketclient = accept(socketport, NULL, NULL);
    return socketclient;
}
```

The first argument to the system call accept() is a socket descriptor. The second argument could be a pointer to the address of another socket. Here socketport has already been bound to a local port and marked for listening. Therefore, the second argument must be given as NULL. The third argument, which is the size of the struct second argument points to, must also be NULL. By default, the system call accept() blocks until a connection is made. It returns a socket called socketclient here. The operating system kernel can use this socket to find out the IP address of the client as well as the port numbers at the client and server for this connection. The port number 28537 was used by the server to listen for connections. Once a connection is made, the connection gets a different port number on the server as well as the client. Port numbers are generated dynamically by the Linux kernel. If the server is multithreaded, it may accept new connections when it is servicing clients.

After connecting to a client, the server runs the following function:

```
void partialsum_server(int socket2, int blocksize){
    double *recvbuf = new double[blocksize];
    double *sendbuf = new double[blocksize];
```