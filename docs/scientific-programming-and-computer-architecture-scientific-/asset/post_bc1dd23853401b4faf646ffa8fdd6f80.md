
# 484 Chapter 6. Special Topic: Networks and Message Passing

tage is to hide the conversion of the port number from host to network format (most likely little endian to big endian format).

The system call listen() on line 13 marks the socket for listening with a backlog of 10. The system socketport will keep up to 10 clients waiting for a connection but no more. The system call listen() is nonblocking. It does not actually listen.

Lines 15 and 16 use setsockopt() to ensure that the port address can be safely reused after the server is shut down. This function returns the socket file descriptor socketport (line 17).

Many servers have firewalls that block incoming connections on all ports a chosen few. For this program to work, the firewall must be modified to accept connections on port 28537.

Once the socket has been bound to a port and marked for listening, it is ready to accept connections.

```c
int connect2(int socketport){
    int socketclient;
    socketclient = accept(socketport, NULL, NULL);
    return socketclient;
}
```

The first argument to the system call accept() is a socket descriptor. The second argument could be a pointer to the address of another socket. Here socketport has already been bound to a local port and marked for listening. Therefore, the second argument must be given as NULL. The third argument, which is the size of the struct second argument points to, must also be NULL. By default, the system call accept() blocks until a connection is made. It returns a socket called socketclient here. The operating system kernel can use this socket to find out the IP address of the client as well as the port numbers at the client and server for this connection. The port number 28537 was used by the server to listen for connections. Once a connection is made, the connection gets a different port number on the server as well as the client. Port numbers are generated dynamically by the Linux kernel. If the server is multithreaded, it may accept new connections when it is servicing clients.

After connecting to a client, the server runs the following function:

```c
void partialsum_server(int socket2, int blocksize){
    double *recvbuf = new double[blocksize];
    double *sendbuf = new double[blocksize];
```

```c
4    double S=0;
5    while(1){
6        int ncrev=block_recv(sock2client, recvbuf,
7                               8*blocksize);
8        if(ncrev==0)
9            break;
10       for(int i=0; i < blocksize; i++){
11            S += recvbuf[i];
12            sendbuf[i] = S;
13       }
14       block_send(sock2client, sendbuf, 8*blocksize);
15   }
16   close(sock2client);
17   delete[] recvbuf;
18   delete[] sendbuf;
19 }
```

This function uses the variable S defined on line 4 to keep track of partial sums. On line 6, it receives blocksize double-precision numbers in the buffer recvbuf[] (allocated on line 2). If the returned value ncrev is zero, the client has terminated the connection and the server breaks out of the while-loop on line 9. If it receives a block of numbers, it updates the partial sum and stores it in sendbuf[] (lines 11 and 12). The array of partial sums is sent back to the client (line 13).

The server invokes the following function:

```c
void server(int blocksize){
    int sock2port= bind2port(PORTNUM);
    while(1){
        int sock2client = connectclient(sock2port);
        partialsum_server(sock2client, blocksize);
    }
}
```

This function binds to the port 28537 (which is the value of PORTNUM) and listens for connections. As soon as it makes a connection to a client, it calls partialsum_server().

## 6.4.4 Client

The client mirrors the server in some ways but differs in others. The client begins by establishing a connection with the server.

```c
1 int connect2server(const char *server,
2 const char *portnum){
3 struct addrinfo hint;
4 memset(&hint, 0, sizeof(hint));
5 hint.ai_family = AF_UNSPEC;
6 hint.ai_socktype = SOCK_STREAM;
7 struct addrinfo *list;
8 getaddrinfo(server, portnum, &hint, &list);
9 int sock2server = socket(list->ai_family,
10 list->ai_socktype,
11 list->ai_protocol);
12 connect(sock2server, list->ai_addr,
13 list->ai_addrlen);
14 freeaddrinfo(list);
15 return sock2server
16 }
```

The argument server (line 1) is the name of machine on which the server is running. It could be login.univ.edu, for example. The hint (line 3) specifies the family but not the address. The call to getaddrinfo() on line 7 gives the name of the server but also specifies a port number. The specified port number is the second argument to this function. It opens a socket on lines 9, 10, and 11. The socket sock2server is connected to the server on lines 12 and 13 using connect(). There is some subtlety in the ways connections are established and terminated over the Internet that is not discussed here. The system call connect() is the client-side counterpart of accept(). The second argument to connect() is of type sockaddr*. The struct it points to (*list) has information about the IP address of the server as well as the port number on which it is expected to listen. That of course is structured by getaddrinfo() (line 8). In general, getaddrinfo() returns a linked list of structs. In principle, for robustness, we must loop through entries of that list until a connection attempt succeeds with one of them. For reasons given earlier, no attempt is made to detect and handle error.

To find the partial sums of series, the client uses the following program:

```c
void partialsum_client(int sock2server,
    double *series, int n,
    int blocksize,
    double *psum,
    StatVector& stat_ts,
    StatVector& stat_tr){
  assert(n%blocksize==0);
  int count = n/blocksize;
  double cycles;
  Timestamp clk;
  for(int i=0; i < count; i++){
    clk.tick();
    int nsend=block_send(sock2server, series,
        8*blocksize);
    cycles = clk.toc();
    stat_ts.insert(cycles);
    clk.tick();
    int nrecv=block_recv(sock2server, psum,
        8*blocksize);
    cycles = clk.toc();
    stat_tr.insert(cycles);
    series += blocksize;
    psum += blocksize;
  }
  close(sock2server);
}
```

There is not much new to say here. The client alternately calls block_send() to send a block of series[] and block_recv() to store the partial sums in psum[]. The calls to block_send() and block_recv() are timed. Statistics for the number of cycles consumed during send and receive are gathered using StatVector objects. The listing of the client program is completed by the following function definition:

```c
void client(const char* server, int blocksize){
    int n;
  if(blocksize < 1000)
    n = 1000*blocksize*10;
  else
    n=1000*1000*20;
    n = (n/blocksize)*blocksize;
    int sock2server = connect2server(server, PORTNUM);
    double *series= new double[n];
    for(int i=0; i < n; i++)
        series[i]=(i*2==0)?4.0/(2*i+1):-4.0/(2*i+1);
    double *psum=new double[n];
    int count = n/blocksize;
    StatVector stat_ts(count), stat_tr(count);
    Timestamp clk;
    clk.tic();
    partialsum_client(sock2server, series, n,
        blocksize, psum, stat_ts, stat_tr);
    double cycles = clk.toc();
    /* output code omitted */
    std::cout<<"bandwidth = " <<16.0*n/cycles*1e9*CPGHZ/1e3
        << "kbps"<<endl;
    delete[] series;
    delete[] psum;
}
```

The first argument is the name of the server.¹⁹. The second argument to client() is blocksize. This argument must have the same value that it does on server() for this program to run correctly. Note that the number of terms in the series is always an even integer multiple of the block size. The array series[] is initialized with the Leibniznseries.

Most of the code for producing output is omitted. But we show the bandwidth calculation, which includes bytes sent as well as received. The constant CPUGHZ must be defined equal to the CPU speed in GHz.

¹⁹To run this program, know the computer that is running the server either in the form www.somewhere.org or as an IP address. There are many web services you can use to find out the IP address of your computer.

## 6.4. The Internet

## 6.4.5 Internet latency

To find the network latency, we take the block size to be 100 double-precision numbers or 800 bytes. Such a block fits comfortably within a single TCP/IP packet smaller than 1.5 KB (Ethernet MTU). Thus, the client sends a single TCP/IP packet and waits for the partial sums, which arrive in a single TCP/IP packet.

All measurements were performed by running the server at the Texas Advanced Computing Center (TACC) and the client at the University of Michigan (UM). The median time for send + recv was close to 55 milliseconds in several trials. Therefore, we may take the round trip latency between UM and TACC to be 55 milliseconds is a fascinating problem.

Understanding why the latency is 55 milliseconds the distance from UM to TACC is more than 1,000 miles. Therefore, the velocity of light seems to account for more than 10 milliseconds of the latency.

In facts, things are more complicated. The Linux command traceroute shows that the packets take a different route from UM to TACC and the way back A packet from UM to TACC travels from the author's desktop to a router located 2.3 miles almost immediately (after several hops). The router 2.3 miles south of the author's desktop is managed by Merit Networks. From that router, it jumps to a router in Lubbock, covering most of the distance from UM to TACC in a single hop. The router in Lubbock, is managed by LEARN. The packet travels from Lubbock, Texas, to a TACC router in several quick hops. Much of the latency

> ²20Thanks to Barnar (email except) for a July 2005 post on a Comcast forum explaining a few of the intricacies of traceroute.
