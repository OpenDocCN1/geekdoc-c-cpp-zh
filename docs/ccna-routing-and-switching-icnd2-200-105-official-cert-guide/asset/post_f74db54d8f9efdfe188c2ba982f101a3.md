
## The Physical Components of a Leased Line

To create a leased line, the telco must create some physical transmission path between the two routers on the ends of the link. The physical cabling must leave the buildings where each router sits. Then the telco must create the equivalent of a two-pair circuit from end to end, with one circuit to send data in each direction (full duplex). Figure 13-3 shows one such example, in which the telco uses a couple of traditional central office (CO) switches to create a short leased line between two routers.

![](img/79473ea15699e01619d2aa789f5bd43b_387_0.png)

The details in the center of Figure 13-3 probably show more than you ever need to know about leased-line WANs, at least from the enterprise customer perspective. More commonly, most network engineers think more about a leased line from the perspective of Figure 13-4, which shows a few key components and terms for the equipment on the ends of a leased line, as follows:

- **Customer premises equipment (CPE):** This telco term refers to the gear that sits at their customers' sites on the ends of the link.
- **Channel service unit/data service unit (CSU/DSU):** This device provides a function called *clocking*, in which it physically controls the speed and timing at which the router serial interface sends and receives each bit over the serial cable.
- **Serial cable:** This is a short cable that connects the CSU and the router serial interface.

![](img/79473ea15699e01619d2aa789f5bd43b_387_1.png)

The CPE includes several separately orderable parts. When using an external CSU/DSU, a serial cable must be used to connect the CSU to the router serial interface. These serial interfaces usually exist as part of a removable card on the router, called either WAN interface cards (WIC), high-speed WICs (HWIC), or Network Interface Modules (NIM).

Back in the 1950s and 1960s, the U.S.-based Bell companies developed and deployed digital voice and the T-carrier system. As part of that work, they standardized different transmission speeds, including 64 Kbps, 1.544 Mbps, and 44.736 Mbps.

Those same Bell companies developed time-division multiplexing (TDM) technology that let them combine multiples of these base speeds onto a single line. For instance, one popular standard, a Digital Signal level 1 (DS1), or T1, combines 24 DS0s (at 64 Kbps) plus 8 Kbps of overhead into one physical line that runs at 1.544 Mbps. However, to allow flexibility of speeds offered to customers, the telco could install a T1 line to many sites, but run some at slower speeds and some at faster speeds—as long as those speeds were multiples of 64 Kbps.

Now back to the idea of the speed of a leased line. What can you actually buy? Basically, at slower speeds, you get any multiple of 64 Kbps, up to T1 speed. At faster speeds, you can get multiples of T1 speed, up to T3 speed. Table 13-3 summarizes the speeds typically seen in the United States, with a few from Europe.

**Table 13-3** *WAN Speed Summary*

| Names of Line | Bit Rate |
| --- | --- |
| DS0 | 64 Kbps |
| Fractional T1 | Multiples of 64 Kbps, up to 24X |
| DS1 (T1) | 1.544 Mbps (24 DS0s, for 1.536 Mbps, plus 8 Kbps overhead) |
| E1 (Europe) | 2.048 Mbps (32 DS0s) |
| Fractional T3 | Multiples of 1.536 Mbps, up to 28X |
| DS3 (T3) | 44.736 Mbps (28 DS1s, plus management overhead) |
| E3 (Europe) | Approx. 34 Mbps (16 E1s, plus management overhead) |

### The Role of the CSU/DSU

For our last bit of discussion about WAN links in a working enterprise internetwork, next consider the role of the CSU/DSU (called CSU for short). For the sake of discussion, the next few paragraphs, leading up to Figure 13-7, assume a leased line with external CSU/DSUs, like earlier in Figure 13-4.

The CSU sits between the telco leased line and the router; it understands both worlds and their conventions at Layer 1. On the telco side, that means the CSU connects to the line from the telco, so it must understand all these details about the T-carrier system, TDM, and the speed used by the telco. On the router side of the equation, the CSU connects to the router, with roles called the DCE and DTE, respectively. The CSU, acting as DCE (data circuit-terminating equipment), controls the speed of the router serial interface. The router, acting as DTE (data terminal equipment), is controlled by the clocking signals from the CSU (DCE). That is, the CSU tells the router when to send and receive bits; the router attempts to send and receive bits only when the DCE creates the correct electrical impulses (called clocking) on the cable. Figure 13-7 shows a diagram of those main concepts of the role of the CSU/DSU.

![](img/79473ea15699e01619d2aa789f5bd43b_390_0.png)

![](img/79473ea15699e01619d2aa789f5bd43b_390_1.png)

**Figure 13-7** *DCE and DTE Roles for a CSU/DSU and a Router Serial Interface*

### Building a WAN Link in a Lab

On a practical note, to prepare for the CCENT and CCNA R&S exams, you might choose to buy some used router and switch hardware for hands-on practice. If you do, you can create the equivalent of a leased line, without a real leased line from a telco, and without CSU/DSUs, just using a cabling trick. This short discussion tells you enough information to create a WAN link in your home lab.

First, when building a real WAN link with a real telco facility between sites, the serial cables normally used between a router and an external CSU/DSU are called DTE cables. That is, the serial cables in earlier Figure 13-4 are DTE cables.

You can create an equivalent WAN link just by connecting two routers' serial interfaces using one DTE cable and a slightly different DCE cable, with no CSUs and with no leased line from the telco. The DCE cable has a female connector, and the DTE cable has a male connector, which allows the two cables to be attached directly. That completes the physical connection, providing a path for the data. The DCE cable also does the equivalent of an Ethernet crossover cable by swapping the transmit and receive wire pairs, as shown in Figure 13-8.

![](img/79473ea15699e01619d2aa789f5bd43b_390_2.png)

**Figure 13-8** *Serial Cabling Uses a DTE Cable and a DCE Cable*

The figure shows the cable details at the top, with the wiring details at the bottom. In particular, at the bottom of the figure, note that the DTE serial cable acts as a straight-through cable and does not swap the transmit and receive pair, whereas the DCE cable does swap the pairs.

> **NOTE** Many vendors, for convenience, sell a single cable that combines the two cables shown in Figure 13-8 into a single cable. Search online for "Cisco serial crossover" to find examples.

Finally, to make the link work, the router with the DCE cable installed must provide clocking. A router serial interface can provide clocking, but it can do so only if a DCE cable is connected to the interface and by the configuration of the clock rate command. Newer IOS versions will sense the presence of a DCE cable and automatically set a clock rate, so that the link will work, but old IOS versions require that you configure the clock rate command.

### Layer 2 Leased Lines with HDLC

A leased line provides a Layer 1 service. It promises to deliver bits between the devices connected to the leased line. However, the leased line itself does not define a data link layer protocol to be used on the leased line. HDLC provides one option for a data link protocol for a leased line.

HDLC has only a few big functions to perform with the simple point-to-point topology of a point-to-point leased line. First, the frame header lets the receiving router know that a new frame is coming. Plus, like all the other data link protocols, the HDLC trailer has a Frame Check Sequence (FCS) field that the receiving router can use to decide whether the frame had errors in transit, and if so, discard the frame.

Cisco adds another function to the ISO standard HDLC protocol by adding an extra field (a Type field) to the HDLC header, creating a Cisco-specific version of HDLC, as shown in Figure 13-9. The Type field allows Cisco routers to support multiple types of network layer packets to cross the HDLC link. For example, an HDLC link between two Cisco routers can forward both IPv4 and IPv6 packets because the Type field can identify which type of packet is encapsulated inside each HDLC frame.

![](img/79473ea15699e01619d2aa789f5bd43b_391_0.png)

**Figure 13-9** *Cisco HDLC Framing*

Today, the HDLC Address and Control fields have little work to do. For instance, with only two routers on a link, when a router sends a frame, it is clear that the frame is sent to the only other router on the link. Both the Address and Control fields had important purposes in years past, but today they are unimportant.

Routers use HDLC just like any other data link protocol used by routers: to move packets to the next router. Figure 13-10 shows three familiar routing steps, with the role of HDLC sitting at Step 2.

![](img/79473ea15699e01619d2aa789f5bd43b_391_1.png)

**Figure 13-10** *General Concept of Routers De-encapsulating and Re-encapsulating IP Packets*
