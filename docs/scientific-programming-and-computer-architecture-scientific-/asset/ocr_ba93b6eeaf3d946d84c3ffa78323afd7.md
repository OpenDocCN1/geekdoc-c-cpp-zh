# Chapter 6. Special Topic: Networks and Message Passing

```
char *ai_canonname;
struct addrinfo *ai_next;
```

The last field ai_next is a pointer that links to another struct addrinfo object to a linked list. We will explain other fields as they arise. On line 3 of saddrlist(), memset() sets all the fields of the object hint to be zero. Lines 4 and 5 give ai_family and ai_socktype as AF_UNSPEC and SOCK_STREAM, respectively. The address family can be either IPv4 or IPv6. By saying AF_UNSPEC, we are allowing it to be either. The socket type is SOCK_STREAM for TCP. There are other types for datagram and control messages. To an overwhelming extent, the Internet is powered by TCP sockets. We can set it to specific values to restrict the hint to TCP, UDP, or multicast.

The actual call to getaddrinfo() is on line 7 of saddrlist(). The function getaddrinfo() returns 0 on success and various error codes otherwise. Because our objective is to illustrate TCP/IP and no more, we omit all error handling. The first argument inaddr can be NULL, or www.xsede or some other Internet address. The second argument is given as NULL, but specific values can be used to specify services such as http or ssh. The third argument is the pointer to hint. The final argument is the pointer to llist. On line 6 of saddrlist(), the variable llist is defined to be of type struct addrinfo *. On return, it is a pointer to a linked list of struct addrinfo objects, each which holds information about a socket corresponding to the argument inaddr and confirming with the hint.

The function printlist() defined below walks through llist and prints some of the information contained in each node of the linked list.

```
void printlist(struct addrinfo *llist){
    while(llist != NULL) {
        printinfo(llist);
        llist = llist->ai_next;
    }
}
```

The actual printing is done by the function printinfo().

```
1 void printinfo(struct addrinfo *p){
2     char ipver[200];
```