
SPAN solves this problem by copying those frames from certain ports (*SPAN source ports*) to the port where the network analyzer sits (the *SPAN destination port*). Figure 26-16 shows the concept. In this case, the switch has two SPAN source ports, G1/0/11 and G1/0/12. Frames received on both ports are copied out to the SPAN destination port G1/0/21.

![](img/79473ea15699e01619d2aa789f5bd43b_1431_0.png)

**Figure 26-16**  *SPAN Copies (Mirrors) Frames to the Network Analyzer*

First, consider the SPAN example in Figure 26-17. It shows the concept of using port G1/0/11 as a source port. However, the logic goes beyond identifying the source port; it also specifies for the switch to copy frames being transmitted (Tx) out that switch port. The SPAN logic would watch for frames sent out that switch port, and then copy the frames out the SPAN destination port (G1/0/21 in this case).

![](img/79473ea15699e01619d2aa789f5bd43b_1432_0.png)

**Figure 26-17**  *SPAN Construct: Source Port G1/0/11, for Frames in the Transmit Direction*

SPAN configuration actually has quite a few dependencies, with the following list mentioning some of the most important dependencies:

- A SPAN destination port can be used with only one SPAN session at a time.
- A SPAN destination port cannot also be a SPAN source port.
- When configured as a SPAN destination port, the switch no longer treats the port as a normal port. That is, the switch does not learn MAC addresses for received frames, or send frames based on matching the MAC table, for that port.
- A SPAN destination port can be unconfigured from one monitor session (*no monitor session number destination interface type number*) and then added to another monitor session.
- Multiple SPAN sources can be used in a single SPAN session.
- One SPAN session cannot mix interfaces and VLAN sources; that is, the sources must all be interfaces or all be VLANs.
- One SPAN session can use any combination of directions (transmit, receive, and both) as applied to different SPAN sources.
- EtherChannel interfaces can be used as source ports. Frames for all ports in the EtherChannel will be considered by SPAN.
- Trunks can be used as source ports. When used, by default, SPAN includes frames from all VLANs on that trunk, but SPAN VLAN filtering can limit the VLANs included.

## Chapter 27

A VM—that is, an OS instance that is decoupled from the server hardware—still must execute on hardware. Each VM has a configuration, such as the minimum number of vCPUs it needs, minimum RAM, and so on. The virtualization system then starts each VM on some physical server so that enough physical server hardware capacity exists to support all the VMs running on that host. So, at any one point in time, each VM is running on a physical server, using a subset of the CPU, RAM, storage, and NICs on that server. Figure 27-3 shows a graphic of that concept, with four separate VMs running on one physical server.

![](img/79473ea15699e01619d2aa789f5bd43b_1434_0.png)

To get a broader sense of what it means for a service to be a cloud service, examine this list of five criteria for a cloud computing service. The list is derived from the definition of cloud computing as put forth by the U.S. National Institute of Standards and Technology (NIST):

- **On-demand self-service:** The IT consumer chooses when to start and stop using the service, without any direct interaction with the provider of the service.
- **Broad network access:** The service must be available from many types of devices and over many types of networks (including the Internet).
- **Resource pooling:** The provider creates a pool of resources (rather than dedicating specific servers for use only by certain consumers), and dynamically allocates resources from that pool for each new request from a consumer.
- **Rapid elasticity:** To the consumer, the resource pool appears to be unlimited (that is, it expands quickly, so it is called *elastic*), and the requests for new service are filled quickly.
- **Measured service:** The provider can measure the usage and report that usage to the consumer, both for transparency and for billing.

With Software as a Service (SaaS), the consumer receives a service with working software. The cloud provider may use VMs, possibly many VMs, to create the service, but those are hidden from the consumer. The cloud provider licenses, installs, and supports whatever software is required. The cloud provider then monitors performance of the application. However, the consumer chooses to use the application, signs up for the service, and starts using the application—no further installation work required. Figure 27-11 shows these main concepts.

![](img/79473ea15699e01619d2aa789f5bd43b_1437_0.png)

**Figure 27-11** *SaaS Concept*

The primary reasons to choose one PaaS service over another, or to choose a PaaS solution instead of IaaS, are the mix of development tools. Without experience as a developer, it can be difficult to tell whether one PaaS service might be better. You can still make some choices about sizing the PaaS VMs, similar to IaaS tools when setting up some PaaS services, as shown in Figure 27-12, but the developer tools included are the key to a PaaS service.

![](img/79473ea15699e01619d2aa789f5bd43b_1438_0.png)

**Figure 27-12** *PaaS Concept*

Using the Internet as the WAN connectivity to a public cloud is both a blessing and a curse in some ways. Using the Internet can help you get started with public cloud and get working quickly, but it also means that you do not have to do any planning before deploying a public cloud service. With a little planning, a network engineer can see some of the negatives of using the Internet—the same negatives when using the Internet for other purposes—which then might make you want to use alternative WAN connections. Those negatives for using the Internet for public cloud access are:

- **Security:** The Internet is less secure than private WAN connections in that a “man in the middle” can attempt to read the contents of data that passes to/from the public cloud.
- **Capacity:** Moving an internal application to the public cloud increases network traffic, so the question of whether the enterprise’s Internet links can handle the additional load needs to be considered.
- **Quality of Service (QoS):** The Internet does not provide QoS, whereas private WANs can. Using the Internet may result in a worse user experience than desired, because of higher delay (latency), jitter, and packet loss.
- **No WAN SLA:** ISPs typically will not provide a service level agreement (SLA) for WAN performance and availability to all destinations of a network. WAN service providers are much more likely to offer performance and availability SLAs.

Table 27-2 summarizes some of these key pros and cons for the public WAN options for cloud computing, for study and reference.

**Table 27-2**  *Comparison of Key Pros and Cons*

|  | Internet | Internet VPN | MPLS VPN | Ethernet WAN | Intercloud Exchange |
|---|---|---|---|---|---|
| Secure | No | Yes | Yes | Yes | Yes |
| QoS | No | No | Yes | Yes | Yes |
| Requires capacity planning | Yes | Yes | Yes | Yes | Yes |
| Easier migration to new provider | Yes | Yes | No | No | Yes |
| Can begin using public cloud quickly | Yes | Yes | No | No | No |

## Chapter 28

Now broaden your thinking for a moment, and try to think of everything a router or switch might do when receiving, processing, and forwarding a message. Of course, the forwarding decision is part of the logic; in fact, the data plane is often called the *forwarding plane*. But think beyond matching the destination address to a table. For perspective, the following list details some of the more common actions that a networking device does that fit into the data plane:

- De-encapsulating and re-encapsulating a packet in a data link frame (routers, Layer 3 switches)
- Adding or removing an 802.1Q trunking header (routers and switches)
- Matching the destination MAC address to the MAC address table (Layer 2 switches)
- Matching the destination IP address to the IP routing table (routers, Layer 3 switches)
- Encrypting the data and adding a new IP header (for VPN processing)
- Changing the source or destination IP address (for NAT processing)
- Discarding a message due to a filter (ACLs, port security)
