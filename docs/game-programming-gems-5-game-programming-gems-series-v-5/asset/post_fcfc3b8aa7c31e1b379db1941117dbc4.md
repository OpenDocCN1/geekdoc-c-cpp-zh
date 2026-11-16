
10.0.0.2 port 6000, this port number should remain allocated for that address/port pair for as long as the connection is open, or a returning packet addressed to 81.226.155.187:11001 will not make it back to the right place.

Third parties cannot send traffic to the internal node, because the private address of the internal node makes no sense when interpreted in the open Internet; a packet addressed to 10.0.0.2 from the outside would not even make it to the gateway. Similarly, if a packet arrives at the NAT router with a source address or port that the internal node has not recently sent data to, there will be no tuple recorded in the gateway to translate the destination address to an internal address, and the gateway will simply drop the packet. In this way, a NAT router works a lot like a stateful firewall and often provides all the protection a typical home user needs from remote network attacks. It still cannot protect against attacks that rely on user behavior, such as sending Trojans through e-mail or enticing the user to click on malicious Web links, but it is a good first defense.

![](img/672fe9a2d008ba627b1991e15d70f43e_699_0.png)

| Internal Address | Public Address | Destination |
|---|---|---|
| 10.0.0.2:6000 | 81.226.155.187:1101 | 64.125.216.191:80 |
| 10.0.0.2:53 | 81.226.155.87:53 | 195.67.199.27:53 |
| 10.0.0.2:53 | 81.226.155.87:53 | 195.67.199.28:53 |
| 10.0.0.4:53 | 81.226.155.87:11002 | 195.67.199.27:53 |

FIGURE 6.5.2 Example NAT-ed Internet connection.

## How Does NAT Break Client/Server Protocols?

The NAT router substitutes a public source address/port pair for the private address/port pair, remembers the destination address/port, and forwards the packet. For returning packets, it does the reverse translation, and the node on the internal network can communicate flawlessly with the outside world.

Unfortunately, this does not work for all protocols, especially protocols designed before NAT gained wide acceptance, or without proper understanding of the needs of NAT. One prime example is the File Transfer Protocol (FTP) that is commonly used to download files on the Internet. When FTP was designed, it was designed so that one node could set up a file transfer between two other nodes [RFC959], [RFC1123]. The controlling node C would connect to node A, tell node A to expect a file, node A would start listening on a port, and tell node C what this port is. Node C would then connect node B, and tell node B to connect to node A on that port, sending the file. This also allows the control connection to remain open and issue more commands while data is being transferred on the data connection.

The common case of transferring a file to the controlling node C from the server node B is handled as a special case in the FTP protocol, where the port and address of node C are forwarded to node B, and node B connects back to node C to actually send the data.

The problem is that, because the receiving node listens on a port, rather than actively connecting to the external server, if a NAT router is in the way, the local port and address of node C makes no sense to node B when instructed to connect back. The NAT router translates the source address of the outgoing request to connect back to node C, but it does not have any knowledge of the actual data stream inside the FTP control connection, and thus the internal address and port of the socket waiting for the connection passes through untouched as data on the wire.

An example of how a UDP-based game may make the same mistake as the FTP protocol is found in Listing 6.5.1.

### Listing 6.5.1 Embedded Address Code Sample

```
/* An example packet structure for
// connecting to a server.
struct CmdHello {
    char cmd;
    char len;
    unsigned short port;
    unsigned int addr;
};
// Get the local address of a socket; this is not
// something that's generally
// useful on the public internet!
struct sockaddr_in addr;
socklen_t len;
len = sizeof(addr);
rc = getsockname(sock, (struct sockaddr *)&addr,
&len);
// This bad code puts a local address into
// a packet sent to a remote location - do
// NOT do this yourself
Hello h;
h.cmd = CMD_HELLO;
h.len = sizeof(h);
h.port = addr.sin_port; // don't do this!
h.addr = addr.sin_addr; // don't do this!
sendto(sock, &h, h.len, 0,
serverAddr, sizeof(serverAddr));
```

### The Hack

Because FTP is a very common protocol with lots of clients in use, a fix had to be found. Ideally, that fix would not require changing all FTP clients in existence.

The fix that emerged involves adding smarts to the NAT router and having it inspect the data of packets of traffic to certain ports. Most NAT routers today know enough of the FTP control protocol to be able to intercept a control message containing an address and port and rewrite the data of the protocol to contain a public address and port; the router will also add the appropriate tuple in the active NAT session table to allow packets from the serving node to get back in.

While the FTP protocol is so widespread that it enjoys special status in the majority of NAT gateways (but not all), newly designed protocols cannot hope to achieve the same special-case status.

### The Fix

The real fix to make a network protocol NAT safe is to structure the protocol so that IP addresses or port numbers do not need to travel within the data stream. The easiest way to make sure that this is sufficient for the protocol needs is to always create a connection from the client to the server, using UDP or TCP, and always have the server reply back to the client using the address visible on the server when the client connects. No forwarding of connection information should occur over back channels between servers. Correct management of peer addresses is illustrated in Listing 6.5.2.

Some very advanced data center equipment exists that is NAT aware. One kind uses reverse NAT to load-balance connections, secure clusters against external attackers, or allow freedom in assignment and management of IP address space. Design of a communication system involving reverse NAT in the face of shared authentication has to be done with utmost care and is beyond the scope of this gem.

### Listing 6.5.2 Correct Address Management

```
// A proposed packet for acknowledging a
// (corrected) CmdHello packet.
struct CmdHelloAck {
    char cmd;
    char len;
};

// The server uses ::recvfrom() to correctly get the
// address of the peer that connects.
struct sockaddr_in addr;
socklen_t len = sizeof(addr);
union {
    CmdHello hello;
} command;
recvfrom(sock, &command, sizeof(command), 0,
    (struct sockaddr *) &addr, &len);
// Server registers connected client on a received
// hello packet, and then acknowledges using
// ::sendto() to the received address.
if (command.hello.cmd == CMD_HELLO) {
    // client_hello() is the function that adds
    // a newly connected client to some internal list
    client_hello(command.hello, addr);
    CmdHelloAck ack;
    ack.cmd = CMD_HELLO_ACK;
    ack.len = sizeof(ack);
    sendto(sock, &ack, sizeof(ack), 0,
        (struct sockaddr *)addr, sizeof(addr));
}
```

### Other Problems

A variant of this problem is where a game server cluster uses one server for validating logins, and then passes the information about the player to another server, which attempts to return traffic to the client. Even if the public NAT address of the client is used, the NAT router does not expect to see traffic from the new server, so the return traffic is dropped.

Again, the rule to make a protocol fully NAT safe is to always initiate the connection with each individual server from the client, and to never send IP addresses or port numbers as data, but instead rely on ::accept(), ::getpeername(), and ::recvfrom() (but not ::getsockname()!) to get the address of the node on the other end.

To support the idea of a central login server that validates username and password for a server cluster, you could use a cryptographic cookie. Share a common secret (frequently, a 128-bit strong random number) between the servers. When the player logs in, the login server creates a hash of user ID, login time, and the shared secret, and returns user ID, time, and hash to the client. The client then submits this same
