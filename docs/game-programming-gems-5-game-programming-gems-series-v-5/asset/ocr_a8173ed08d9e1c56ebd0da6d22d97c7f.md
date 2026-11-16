# How Does NAT Break Client/Server Protocols?

The NAT router substitutes a public source address/port pair for the private address/ port pair, remembers the destination address/port, and forwards the packet. For returning packets, it does the reverse translation, and the node on the internal network can communicate flawlessly with the outside world.

Unfortunately, this does not work for all protocols, especially protocols designed before NAT gained wide acceptance, or without proper understanding of the needs of NAT. One prime example is the File Transfer Protocol (FTP) that is commonly used to download files on the Internet. When FTP was designed, it was designed so that one node could set up a file transfer between two other nodes [RFC959], [RFC1123]. The controlling node C would connect to node A, tell node A to expect a file, node A would start listening on a port, and tell node C what this port is. Node C would then connect node B, and tell node B to connect to node A on that port, sending the file. This also allows the control connection to remain open and issue more commands while data is being transferred on the data connection.

The common case of transferring a file to the controlling node C from the server node B is handled as a special case in the FTP protocol, where the port and address of node C are forwarded to node B, and node B connects back to node C to actually send the data.

The problem is that, because the receiving node listens on a port, rather than actively connecting to the external server, if a NAT router is in the way, the local port and address of node C makes no sense to node B when instructed to connect back. The NAT router translates the source address of the outgoing request to connect back to node C, but it does not have any knowledge of the actual data stream inside the FTP control connection, and thus the internal address and port of the socket waiting for the connection passes through untouched as data on the wire.

An example of how a UDP-based game may make the same mistake as the FTP protocol is found in Listing 6.5.1.

# Listing 6.5.1 Embedded Address Code Sample

```
1: Embedded Address Code Sample/ * An example packet structure for
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
```