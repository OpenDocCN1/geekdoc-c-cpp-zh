
# DISTRIBUTED SYSTEMS

# 633

```c
// client code
int main(int argc, char *argv[]) {
    int sd = UDP_Open(20000);
    struct sockaddr_in addrSnd, addrRcv;
    int rc = UDP_FillSockaddr(&addrSnd, "cs.wisc.edu", 10000);
    char message[BUFFER_SIZE];
    sprintf(message, "hello world");
    rc = UDP_Write(sd, &addrSnd, message, BUFFER_SIZE);
    if (rc > 0) {
        int rc = UDP_Read(sd, &addrRcv, message, BUFFER_SIZE);
    }
    return 0;
}

// server code
int main(int argc, char *argv[]) {
    int sd = UDP_Open(10000);
    assert(sd > -1);
    while (1) {
        struct sockaddr_in addr;
        char message[BUFFER_SIZE];
        int rc = UDP_Read(sd, &addr, message, BUFFER_SIZE);
        if (rc > 0) {
            char reply[BUFFER_SIZE];
            sprintf(reply, "goodbye world");
            rc = UDP_Write(sd, &addr, reply, BUFFER_SIZE);
        }
    }
    return 0;
}
```

> Figure 48.1: Example UDP Code (client.c, server.c)

Once, it is possible that the memory within the router cannot accommodate all of the packets. The only choice the router at that point is to drop one or more of the packets. This behavior occurs at hosts as well; when you send a large number of messages to a single machine, the machine’s resources can easily become overwhelmed, and thus packet loss occurs again.

Thus, packet loss is fundamental in networking. The question becomes: how should we deal with it?

## 4.2 Unreliable Communication Layers

One way is this: we don't deal with it. Because some applications know how to deal with packet loss, it is sometimes useful to let them communicate with a basic unreliable messaging layer, an example of the end-to-end argument one hears often about (see the Aside end of chapter). One excellent example of such an unreliable layer is found

© 2008–19, ARPACI-DUSSEAU

THREE
EASY
PIECES

634

DISTRIBUTED SYSTEMS

```c
int UDF_Open(int port) {
    int sd;
    if ((sd = socket(AF_INET, SOCK_DGRAM, 0)) == -1) {
        return -1;
    }
    struct sockaddr_in myaddr;
    bzero(&myaddr, sizeof(myaddr));
    myaddr.sin_family = AF_INET;
    myaddr.sin_port = htons(port);
    myaddr.sin_addr.s_addr = INADDR_ANY;
    if (bind(sd, (struct sockaddr *) &myaddr, sizeof(myaddr)) == -1) {
        return -1;
    }
    return sd;
}
```

```c
int UDF_FillSockAddr(struct sockaddr *addr, int port) {
    char *hostname, sizeof(struct sockaddr_in);
    addr->sin_family = AF_INET; // host byte order
    addr->sin_port = htons(port); // network byte order
    struct in_addr *in_addr;
    struct hostent *host_entry;
    if ((host_entry = gethostbyname(hostname)) == NULL) {
        return -1;
    }
    in_addr = (struct in_addr *) host_entry->h_addr;
    addr->sin_addr = *in_addr;
    return 0;
}
```

```c
int UDF_Write(int sd, struct sockaddr_in *addr, int n) {
    char *buffer;
    int addr_len = sizeof(struct sockaddr_in);
    return sendto(sd, buffer, n, 0, (struct sockaddr *) addr, addr_len);
}
```

```c
int UDF_Read(int sd, struct sockaddr_in *addr, int n) {
    char *buffer;
    int len = sizeof(struct sockaddr_in);
    return recvfrom(sd, buffer, n, 0, (struct sockaddr *) addr, (socklen_t *) &len);
}
```

Figure 48.2: A Simple UDP Library (udp.c)

OPERATING
SYSTEMS
[Version 1.01]

WWW.OSTEP.ORG

# DISTRIBUTED SYSTEMS

# 635

> TIP: USE CHECKSUMS FOR INTEGRITY
Checksums are a commonly-used method to detect corruption quickly and effectively in modern systems. A simple checksum is addition: just sum the bytes of a chunk of data; or many more sophisticated codes have been created, including basic cyclic redundancy codes (CRCs), the Fletcher, and many others [MK09]. In networking, checksums are used as follows. Before sending a message from one machine to another, compute a checksum over the bytes of the message; Then send the message and the checksum to the destination.

