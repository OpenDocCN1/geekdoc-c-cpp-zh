# Listing 6.5.2 Correct Address Management

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
:recvfrom(sock, &command, sizeof(command), 0,
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
    :sendto(sock, &ack, sizeof(ack), 0,
        (struct sockaddr *)addr, sizeof(addr));
}
```

# Other Problems

A variant of this problem is where a game server cluster uses one server for validating logins, and then passes the information about the player to another server, which attempts to return traffic to the client. Even if the public NAT address of the client is used, the NAT router does not expect to see traffic from the new server, so the return traffic is dropped.

Again, the rule to make a protocol fully NAT safe is to always initiate the connection with each individual server from the client, and to never send IP addresses or port numbers as data, but instead rely on ::accept(), ::getpeername(), and ::recvfrom() (but not ::getsockname()!) to get the address of the node on the other end.

To support the idea of a central login server that validates username and password for a server cluster, you could use a cryptographic cookie. Share a common secret (frequently, a 128-bit strong random number) between the servers. When the player logs in, the login server creates a hash of user ID, login time, and the shared secret, and returns user ID, time, and hash to the client. The client then submits this same