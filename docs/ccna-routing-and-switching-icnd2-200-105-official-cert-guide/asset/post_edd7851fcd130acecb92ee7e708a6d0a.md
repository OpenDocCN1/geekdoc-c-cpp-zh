
For example, the VPN tunnel shown for PC A in Figure 15-7 uses the AnyConnect Client to create a client VPN. The AnyConnect Client creates an SSL tunnel to the ASA firewall that has been installed to expect VPN clients to connect to it. The tunnel encrypts all traffic, so that PC A can use any application available at the enterprise network on the right.

![](img/79473ea15699e01619d2aa789f5bd43b_452_0.png)

**Figure 15-7** *Client VPN Options (SSL)*

Note that while the figure shows an ASA firewall used at the main enterprise site, many types of devices can be used on the server side of an SSL connection as well. The web server itself can be the endpoint of an SSL connection from a web browser, but often, to improve server performance, the SSL tunnel on the server side terminates on specialized devices like the Cisco ASA or a router.

The bottom of Figure 15-7 shows a client VPN that supports a web application for a single web browser tab. The experience is much like when you connect to any other secure website today: the session uses SSL, so all traffic sent to and from that web browser tab is encrypted with SSL. Note that PC B does not use the AnyConnect Client; the user simply opens a web browser to browse to server S2. However, by using SSL, that one session is encrypted with SSL, providing better security.

## GRE Tunnels and DMVPN

The device on the endpoint of an Internet VPN takes a normal unencrypted packet and performs several functions before forwarding that packet. One of those functions is to encrypt the packet, and another is to encapsulate the packet in a new IP header. The new IP header uses addresses in the unsecured network (usually the Internet), allowing the routers between the two VPN tunnel endpoints to forward the VPN IP packet. The original IP packet, including the original IP header, is encrypted and unreadable.

This second major section of this chapter examines a subset of the work to create that kind of site-to-site VPN tunnel. In particular, this section looks at how to set up the tunnel, while ignoring the encryption function. Specifically, this section looks at the concepts and configuration of how routers create a tunnel, encapsulating the original IP packet inside another IP packet. The goal is to give you some general ideas about how tunneling works, while leaving the detailed security configuration to other certifications like CCNA Security.

This section concludes with a short discussion of Dynamic Multipoint VPN (DMVPN). DMVPN helps solve some shortcomings with deploying point-to-point GRE tunnels on a larger scale.

**Key Topic**

![](img/79473ea15699e01619d2aa789f5bd43b_456_0.png)

*Figure 15-12* Encapsulating the Original IP Packet in a GRE-Formatted Packet

While this packet passes through the Internet, the routers in the Internet use this outer GRE delivery IP header to route the packet. The fact that this packet happens to hold another entire IP packet inside does not matter to the IP forwarding process in those routers; they just forward the IP packet based on the 2.2.2.2 destination IP address. Figure 15-13 shows the concept. Note that this packet may be routed by many routers in the Internet before arriving at R2.

![](img/79473ea15699e01619d2aa789f5bd43b_456_1.png)

*Figure 15-13* Internet Routers Forwarding GRE IP Packet Based on Public IP Addresses

When the GRE packet in Figure 15-13 finally arrives on the right side of the Internet, at R2, R2 needs to extract the original IP packet. With physical links, R2 would normally simply remove the old incoming data link header. With a GRE-encapsulated packet, the receiving router (R2) also needs to remove the delivery header and the GRE header, leaving the original packet, as shown in Figure 15-14.

![](img/79473ea15699e01619d2aa789f5bd43b_456_2.png)

*Figure 15-14* Destination Tunnel Endpoint Decapsulates the Original Packet and Forwards It

> **NOTE** If the routers also configured the IPsec encryption part of the tunnel, just after the steps shown in Figure 15-14, the receiving router would then decrypt the original packet.

### Configuring GRE Tunnels

Configuring GRE tunnels requires only a few commands. The challenge with GRE configuration comes in organizing the configuration parameters. The configuration requires a tunnel interface, with IP addresses from the secure part of the network configured with the `ip address` interface command. It also requires that the two routers declare both their own IP address (source) and the other router's IP address (destination), used in the unsecure part of the network. Figure 15-15 shows the organization of the various configuration parameters.

![](img/79473ea15699e01619d2aa789f5bd43b_457_0.png)

**Figure 15-15** *GRE Tunnel Configuration: Relationship of Parameters*

The following list details the configuration steps on each router:

- **Step 1.** Use the `interface tunnel number` global command to create a tunnel interface. The interface numbers have local meaning only and do not have to match between the two routers.
- **Step 2.** (Optional) Use the `tunnel mode gre ip` interface subcommand in tunnel interface mode to tell IOS to use GRE encapsulation on the tunnel. (This is the default setting for a tunnel interface.)
- **Step 3.** Use the `ip address address mask` interface subcommand to assign an IP address to the tunnel interface, using a subnet from the secure network's address range. The two routers on the tunnel should use addresses from the same subnet.
- **Step 4.** Configure the tunnel's source IP address in the unsecure part of the network in one of two ways. Regardless of the method, the local router's source IP address must match the other router's tunnel destination.
  - **Step 4A.** Use the `tunnel source ip-address` tunnel interface subcommand to directly set the tunnel's source IP address.
  - **Step 4B.** Use the `tunnel source interface-id` tunnel interface subcommand to indirectly set the tunnel's source IP address by referencing an interface on the local router.

The `show interfaces tunnel` *interface-number* command lists many counters plus the configuration settings, in addition to the interface status. Example 15-4 lists a sample, again for R1's Tunnel0 interface. Note that it lists the local router (R1) configuration of the source (1.1.1.1) and destination (2.2.2.2) IP addresses, and it confirms the use of GRE encapsulation over IP (IPv4), as highlighted in the example.

**Example 15-4 Tunnel Interface Details**

```text
R1# show interfaces tunnel0
Tunnel0 is up, line protocol is up
  Hardware is Tunnel
  Internet address is 10.1.3.1/24
  MTU 17916 bytes, BW 100 Kbit/sec, DLY 50000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation TUNNEL, loopback not set
  Keepalive not set
  Tunnel source 1.1.1.1 (Serial0/0/0), destination 2.2.2.2
  Tunnel Subblocks:
     src-track:
        Tunnel0 source tracking subblock associated with Serial0/0/0
        Set of tunnels with source Serial0/0/0, 1 member (includes iterators), on
        interface <OK>
  Tunnel protocol/transport GRE/IP
! Lines omitted for brevity
```

Although a working tunnel interface is important, the routers will not use the tunnel interface unless routes try to forward packets over the tunnel interface. The configuration in this example shows that OSPF has been enabled on all interfaces in Class A network 10.0.0.0, the secure part of the internetwork. As a result, the routers should exchange OSPF routes and learn the same routes shown earlier in Figure 15-10. Example 15-5 shows proof, with R1 listing an OSPF-learned route to R2's LAN subnet of 10.1.2.0/24.

**Example 15-5 R1 Routes in Network 10.0.0.0**

```text
R1# show ip route 10.0.0.0
Routing entry for 10.0.0.0/8, 5 known subnets
  Attached (4 connections)
  Variably subnetted with 2 masks
C       10.1.1.0/24 is directly connected, GigabitEthernet0/0
L       10.1.1.0/32 is directly connected, GigabitEthernet0/0
O       10.1.2.0/24 [110/1001] via 10.1.3.2, 00:07:55, Tunnel0
C       10.1.3.0/24 is directly connected, Tunnel0
L       10.1.3.1/32 is directly connected, Tunnel0
! Lines omitted for brevity
```

> **NOTE** The show ip route 10.0.0.0 command lists the known routes inside network 10.0.0.0.
