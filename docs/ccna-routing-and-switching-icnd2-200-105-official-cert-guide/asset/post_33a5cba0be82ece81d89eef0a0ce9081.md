
It might seem like this short topic about IP telephony and switch configuration includes a lot of small twists and turns and trivia, and it does. The most important items to remember are as follows:

- Configure these ports like a normal access port to begin: Configure it as a static access port and assign it an access VLAN.
- Add one more command to define the voice VLAN (`switchport voice vlan vlan-id`).
- Look for the mention of the voice VLAN ID, but no other new facts, in the output of the `show interfaces type number switchport` command.
- Look for both the voice and data (access) VLAN IDs in the output of the `show interfaces type number trunk` command.
- Do not expect to see the port listed in the list of operational trunks as listed by the `show interfaces trunk` command.

## Chapter 2

Table 2-2 summarizes the main three classes of problems that occur when STP is not used in a LAN that has redundancy.

**Table 2-2 — Three Classes of Problems Caused by Not Using STP in Redundant LANs**

| Problem | Description |
|---|---|
| Broadcast storms | The forwarding of a frame repeatedly on the same links, consuming significant parts of the links' capacity. |
| MAC table instability | The continual updating of a switch’s MAC address table with incorrect entries, in reaction to looping frames, resulting in frames being sent to the wrong locations. |
| Multiple frame transmission | A side effect of looping frames in which multiple copies of one frame are delivered to the intended host, confusing the host. |

All other interfaces are placed in blocking state. Table 2-3 summarizes the reasons STP places a port in forwarding or blocking state.

**Table 2-3 — STP: Reasons for Forwarding or Blocking**

| Characterization of Port | STP State | Description |
|---|---|---|
| All the root switch’s ports | Forwarding | The root switch is always the designated switch on all connected segments. |
| Each nonroot switch’s root port | Forwarding | The port through which the switch has the least cost to reach the root switch (lowest root cost). |
| Each LAN’s designated port | Forwarding | The switch forwarding the Hello on to the segment, with the lowest root cost, is the designated switch for that segment. |
| All other working ports | Blocking | The port is not used for forwarding user frames, nor are any frames received on these interfaces considered for forwarding. |

STP defines messages called *bridge protocol data units* (BPDU), which switches use to exchange information with each other. The most common BPDU, called a Hello BPDU, lists many details, including the sending switch’s BID. By listing its own unique BID, switches can tell which switch sent which Hello BPDU. Table 2-4 lists some of the key information in the Hello BPDU.

**Table 2-4 — Fields in the STP Hello BPDU**

| Field | Description |
|---|---|
| Root bridge ID | The bridge ID of the switch the sender of this Hello currently believes to be the root switch |
| Sender’s bridge ID | The bridge ID of the switch sending this Hello BPDU |
| Sender’s root cost | The STP cost between this switch and the current root |
| Timer values on the root switch | Includes the Hello timer, MaxAge timer, and forward delay timer |

Summarizing, the root election happens through each switch claiming to be root, with the best switch being elected based on the numerically lowest BID. Breaking down the BID into its components, the comparisons can be made as

- The lowest priority
- If that ties, the lowest switch MAC address

Figure 2-6 shows an example of how switches calculate their best root cost and then choose their root port, using the same topology and STP costs as shown in Figure 2-5. STP on SW3 calculates its cost to reach the root over the two possible paths by adding the advertised cost (in Hello messages) to the interface costs listed in the figure.

![](img/79473ea15699e01619d2aa789f5bd43b_1203_0.png)

**Figure 2-6** *How STP Actually Calculates the Cost from SW3 to the Root*

Port costs also have default values, per port, per VLAN. You can configure these port costs, or you can use the default values. Table 2-6 lists the default port costs suggested by IEEE. IOS on Cisco switches has long used the default settings as defined in the 1998 version of the 802.1D standard. The newer standard, useful when using links faster than 10 Gbps, can be used by adding a single configuration command to each switch (*spanning-tree pathcost method long*).

**Table 2-6 — Default Port Costs According to IEEE**

| Ethernet Speed | IEEE Cost: 1998 (and Before) | IEEE Cost: 2004 (and After) |
|---|---:|---:|
| 10 Mbps | 100 | 2,000,000 |
| 100 Mbps | 19 | 200,000 |
| 1 Gbps | 4 | 20,000 |
| 10 Gbps | 2 | 2000 |
| 100 Gbps | N/A | 200 |
| 1 Tbps | N/A | 20 |

For various reasons, the convergence process requires the use of three timers. Note that all switches use the timers as dictated by the root switch, which the root lists in its periodic Hello BPDU messages. Table 2-7 describes the timers.

**Table 2-7 — STP Timers**

| Timer | Default Value | Description |
|---|---|---|
| Hello | 2 seconds | The time period between Hellos created by the root. |
| MaxAge | 10 times Hello | How long any switch should wait, after ceasing to hear Hellos, before trying to change the STP topology. |
| Forward delay | 15 seconds | Delay that affects the process that occurs when an interface changes from blocking state to forwarding state. A port stays in an interim listening state, and then an interim learning state, for the number of seconds defined by the forward delay timer. |

When a port that formerly blocked needs to transition to forwarding, the switch first puts the port through two intermediate interface states. These temporary states help prevent temporary loops:

- **Listening:** Like the blocking state, the interface does not forward frames. The switch removes old stale (unused) MAC table entries for which no frames are received from each MAC address during this period. These stale MAC table entries could be the cause of the temporary loops.
- **Learning:** Interfaces in this state still do not forward frames, but the switch begins to learn the MAC addresses of frames received on the interface.

Table 2-8 summarizes spanning tree’s various interface states for easier review.

**Table 2-8 — IEEE 802.1D Spanning-Tree States**

| State | Forwards Data Frames? | Learns MACs Based on Received Frames? | Transitory or Stable State? |
|---|---|---|---|
| Blocking | No | No | Stable |
| Listening | No | No | Transitory |
| Learning | No | Yes | Transitory |
| Forwarding | Yes | Yes | Stable |
| Disabled | No | No | Stable |

RSTP (802.1w) works just like STP (the original 802.1D) in several ways:

- It elects the root switch using the same parameters and tiebreakers.
- It elects the root port on nonroot switches with the same rules.
- It elects designated ports on each LAN segment with the same rules.
- It places each port in either forwarding or blocking state, although RSTP calls the blocking state the discarding state.

The best way to get a sense for these mechanisms is to see how the RSTP alternate port and the backup port both work. RSTP uses the term *alternate port* to refer to a switch’s other ports that could be used as root port if the root port ever fails. The *backup port* concept provides a backup port on the local switch for a designated port, but only applies to some topologies that do not happen often within a modern network design. However, both are instructive about how RSTP works. Table 2-9 lists these RSTP port roles.

**Table 2-9 — Port Roles in 802.1w RSTP**

| Function | Port Role |
|---|---|
| Nonroot switch’s best path to the root | Root port |
| Replaces the root port when the root port fails | Alternate port |
| Switch port designated to forward onto a collision domain | Designated port |
| Replaces a designated port when a designated port fails | Backup port |
| Port that is administratively disabled | Disabled port |
