
while Outparam is received from the RPC server after the RPC body executes. For this difference, we should add parameter direction grammar to our IDL compiler and add code that serializes outparams at the stub and deserializes inparams at the proxy. Here is one example of synchronous RPC.

```
UserLogin([in] string id,[in] string password,
[out] int loginResult);
```

- We need to consider exceptional cases such as timeouts and exceptions, to prevent deadlock.

- We need to manage function call sequence number. When RPC outparam messages are received by the proxy, it can determine which thread is waiting by the call sequence number. To only wake a thread that corresponds to that sequence number, we need to prepare a queue containing outstanding RPC calls waiting for outparam messages.

## Conclusion

Writing an RPC implementation normally has some prerequisites not associated with game programmers. This gem was an attempt to guide you towards getting started with your own RPC system, and you're encouraged to explore and see the productivity and efficiency, as well as performance, you can get via RPC systems. To get the best understanding from this article, you may want to look at some of the references. Now it is your turn!

## References

- [Breck99] eNITL. The Network Improv Template Language. Available online at http://networkimprov.com/lentil/lentil.html.

- [Parr04] Parr, Terence. ANTLR Parser Generator v2.7.4. Available online at http://www.antlr.org.

- [Sebesta02] Sebesta, Robert W. Concepts of Programming Languages 5th Edition, 109–123, 155–159. Addison Wesley, 2002.

- [Silberschatz02] Silberschatz, Galvin, and Gagne, Operating System Concepts 6th Edition, 121–124. Wiley, 2002.

## Overcoming Network Address Translation in Peer-to-Peer Communications

Jon Watte

hplus-gpp5@mindcontrol.org

Peer-to-peer computing revolutionized the way we compute. From the early research Internet of the late 1970s through the dial-up Internet revolution in the early 1990s to today's bonanza of fat broadband pipes, everyone is using computer networking for fun and for profit. More than 50% of all Internet users will have broadband when this gem is published. Although, with this popularity comes all kinds of problems: self-replicating worms, pings of death, and Windows security problems, coupled with heavy vendor scare tactics, cause most users to set up firewalls to protect their computers. Connection-sharing firewalls are a hot selling item, as homes with multiple computers find that sharing a single broadband connection is the easiest route; prices having fallen to under $100 for a feature-rich wireless access point with router, switch, and firewall.

Online games are maybe one of the more exciting applications of computer networking technology, where the ability to compete with players from all over the world from the comfort of your own office, living room, or coffee shop has subtly changed how we view the term "buddy" and how we choose to interact online. Companies like Sony Online Entertainment and NCSoft make it their business to run large server clusters where players from all over the world can meet and play together. However, these big server clusters come with big leasing, power, and networking bills, and such services usually come with a monthly price tag for the end user. Thus, another popular form of online gaming is peer-to-peer gaming, where one player's computer also serves as the server for the game, and all the other players connecting to this player, who is said to be hosting the game.

Unfortunately, some games are not as good at supporting this model of connection as others. Frequently, firewalls and connection sharing software get in the way of hosting games, and sometimes even joining games. While some users may be technical enough to configure a DMZ or port forwarding in their firewalls, many are not. And even for the technical users, pleading with a Starbucks® employee to give you access to their wireless access “hot spot” is unlikely to make that hosted game of Warcraft® III come any closer. As a developer of a networked game, you would like to do better, and this gem will show you how.

### Audience

This chapter is intended for all game programmers who want their game to work as well as possible on the Internet. It is especially important for programmers who want their games to use peer-to-peer, player-hosted servers, and want to extend to as many users as possible without telling users to configure port forwarding, set up a DMZ, or remove their firewall.

We assume that you are familiar with general Berkeley sockets programming (Unix) or Windows WinSock Version 2 (Windows). The technique shown will work equally well under either operating environment. For purposes of this gem, Mac OS X (and higher) works a lot like Unix, but the code has not been verified on Mac OS X. This chapter uses C++ for its code samples, but the techniques can be expressed in any language capable of using networking at the sockets layer.

### IP Addresses

At the core of all networking is the network address. The Internet at large uses an address format called IPv4, which is short for Internet Protocol Version 4. What the first three versions looked like has long since lost its relevance. There is also an up-and-coming version called IPv6 that has so far failed to gain mainstream acceptance. In this article, “IP address” is synonymous with “IPv4 address.”

An IP address is simply a series of four bytes. Typically, it will be written out in dotted notation, such as 192.168.1.2. An IP address identifies a specific network card or modem connected to a specific device on the Internet; these individual hardware devices are called network interfaces.

Devices connected to the Internet may run multiple services; for example, a Web server will often also run a Secure Shell Daemon (SSHD) that allows administrators to access the command-line interface of the server for monitoring and maintenance. To distinguish network packets destined for the Web server from network packets destined for the SSHD, the two most common Internet protocols add the concept of a port number. Each service uses its own port; for Web servers, the port is 80 unencrypted services and 443 for encrypted services. For the SSHD, the port is 22.

For games, the developer will often choose an arbitrary port within the allowable range. Ports in TCP and UDP addresses are two bytes, and thus the range is between 0 and 65535 inclusive, although tradition dictates that the port number is chosen in the range 1024–49151, inclusive. This tradition likely started with the arbitrary implementation choice on Unix, where ports 1 through 1023 are reserved for the special administrative user “root” on the machine, and only root may open new sockets listening for traffic on these ports. For more information, see [Man3resvport] and [RFC793].

A UDP or TCP address thus consists of six bytes: four single-byte numbers in the range 0–255, inclusive, called the IP address, and one two-byte number in the range 0–65535, inclusive, called simply the port. The IP protocol suite specifies that all numbers larger than a single byte be sent with the high-order byte first (big-endian), and most sockets implementations supply functions or macros named htonl(), htons(), ntohl(), and ntohs() to convert between the local machine representation and the well-defined network representation of numbers.

### Sockets Usage

A program running on a machine (we will call these programs “processes” and the machines “nodes” in the rest of this chapter) will typically play one of two roles: server or client. A server process will create a socket using :socket() and bind it to a local port and one of many local addresses if the node has multiple network interfaces, using :bind(). If the socket is used for TCP connections, the server will then call :listen() and enter a loop where it calls :accept() to wait for and accept incoming connections from clients. :accept() returns a new socket for each new client, and data is exchanged using :send() and :recv() using this socket. To tell the different connections apart, each TCP connection on the client side automatically allocates a new, unused port for the specific server connection.

If the socket is instead used for UDP connections, the process will enter a loop where it calls :recvfrom() on the socket directly after :bind(). All incoming traffic from all clients will arrive at the same socket. The network layer has no notion of connectedness, so if multiple, related packets are to be exchanged over UDP, some higher layer software (such as the process itself) has to take care of the coordination thereof.

Return traffic for servers using UDP is usually sent using :sendto().

For a client of a TCP service, after calling :socket(), the process will call :connect() to establish a connection to the intended recipient; once connected, :send() and :recv() are used for data exchange. The argument to :connect() is a TCP address that may have been looked up from a textual name (such as “www.there.com: 80”), using name server functions such as :gethostbyname(). Meanwhile, clients of UDP just call :sendto(), passing in the IP address again, possibly derived from textual form using the name resolution library), and receive data back using :recvfrom().

In a typical process, many things will be going on at the same time, so thinking of “send” and “receive” as sequential events is usually misleading. Physics simulation, graphics drawing, audio mixing, and disk I/O are examples of other actions often happening at the same time as networking in a typical action-oriented networked computer game. The approach to managing these overlapping tasks is usually either
