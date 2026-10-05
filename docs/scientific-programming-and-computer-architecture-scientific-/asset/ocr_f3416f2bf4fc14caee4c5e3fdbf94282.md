# Chapter 6. Special Topic: Networks and Message Passing

socket behavior. The send() may not transmit all the data. It returns the number of bytes transmitted and -1 on error. (lines 4 through 9) repeatedly calls send() until all the data has been sent.

The function for receiving is quite similar.

```
1 int block_recv(int sockfd, void *buf, int len{
2   int total_recv = 0;
3   int num_recv = 0;
4   while(total_recv < len){
5     int nr = recv(sockfd, buf, len-total_recv, 0);
6     if(nr==0){
7       num_recv=0;
8       break;
9     }
10    buf = (char *)buf+nr;
11    total_recv += nr;
12    num_recv += 1;
13  }
14  return num_recv;
15 }
```

There is only one thing to add. If recv() (line 5) returns 0, it is a signal that the opposite party has terminated the connection. Normally, this function executes recv() in a while-loop and returns the total number of receives (line 14). However, if the connection is terminated, it sets num_recv to zero (line 7), breaks out of the loop (line 8), and returns 0, so that the caller knows the connection has been terminated.

# 6.4.3 Server

The server described here receives a sequence of double-precision numbers from its client and sends back their partial sums. Before we get to partial sums, we must explain how the server listens for connections on a designated port. Special port numbers are designated for major applications. For example, http uses port 80 and https uses port 443. On Linux, the list of port numbers in use can be found in the file /etc/services. The port number for our series summing server is taken to be 28537.