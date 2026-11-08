For example, the VPN tunnel shown for PC A in Figure 15-7 uses the AnyConnect Client to create a client VPN. The AnyConnect Client creates an SSL tunnel to the ASA firewall that has been installed to expect VPN clients to connect to it. The tunnel encrypts all traffic, so that PC A can use any application available at the enterprise network on the right.

![](bbox=[0.08, 0.18, 0.92, 0.32])

**Figure 15-7** *Client VPN Options (SSL)*

Note that while the figure shows an ASA firewall used at the main enterprise site, many types of devices can be used on the server side of an SSL connection as well. The web server itself can be the endpoint of an SSL connection from a web browser, but often, to improve server performance, the SSL tunnel on the server side terminates on specialized devices like the Cisco ASA or a router.

The bottom of Figure 15-7 shows a client VPN that supports a web application for a single web browser tab. The experience is much like when you connect to any other secure website today: the session uses SSL, so all traffic sent to and from that web browser tab is encrypted with SSL. Note that PC B does not use the AnyConnect Client; the user simply opens a web browser to browse to server S2. However, by using SSL, that one session is encrypted with SSL, providing better security.

# # GRE Tunnels and DMVPN

The device on the endpoint of an Internet VPN takes a normal unencrypted packet and performs several functions before forwarding that packet. One of those functions is to encrypt the packet, and another is to encapsulate the packet in a new IP header. The new IP header uses addresses in the unsecured network (usually the Internet), allowing the routers between the two VPN tunnel endpoints to forward the VPN IP packet. The original IP packet, including the original IP header, is encrypted and unreadable.

This second major section of this chapter examines a subset of the work to create that kind of site-to-site VPN tunnel. In particular, this section looks at how to set up the tunnel, while ignoring the encryption function. Specifically, this section looks at the concepts and configuration of how routers create a tunnel, encapsulating the original IP packet inside another IP packet. The goal is to give you some general ideas about how tunneling works, while leaving the detailed security configuration to other certifications like CCNA Security.

This section concludes with a short discussion of Dynamic Multipoint VPN (DMVPN). DMVPN helps solve some shortcomings with deploying point-to-point GRE tunnels on a larger scale.