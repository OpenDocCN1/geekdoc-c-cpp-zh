
> **NOTE** In this case, because the **network 192.0.2.0 mask 255.255.255.0** command happens to list a Class C network ID and the default Class C mask, the mask 255.255.255.0 parameter could be omitted. If omitted, IOS assumes a default mask for the address class for the prefix.

Pay close attention to the two **show** commands in the output. The **show ip route 192.0.2.0 255.255.255.0 longer-prefixes** command lists all IPv4 routes in the range of 192.0.2.0 255.255.255.0, one route per line. Note that only one route exists in this range: a route for exactly 192.0.2.0/24, with next-hop address 10.2.2.2 (which is the firewall's IP address).

The **show ip bgp** command lists R1's BGP table, first with several lines of legend, followed by one line for each prefix in the table (only one entry in this case). First, look at the values in the network and next hop columns: it lists the same prefix and next-hop as taken from the IP routing table. Also, of particular importance, note the characters * and > on the far left, which per the legend mean that the route is valid and that this route is the best route to reach this prefix. In cases for which BGP has learned multiple routes to reach one prefix, BGP lists a > beside the best route per the BGP best path algorithm.

Now that R1 has a table entry for the enterprise's public prefix of 192.0.2.0/24, R1 advertises that prefix and associated PAs to its *eBGP* peer. Example 12-5 shows the BGP table and IPv4 routing table on Router ISP1.

**Example 12-5 ISP1's BGP and IP Routing Tables**

```
    ISP1# show ip bgp
    BGP table version is 2, local router ID is 2.2.2.2
    Status codes: s suppressed, d damped, h history, * valid, > best, i - internal,
                  r RIB-failure, S Stale, m multipath, b backup-path, f RT-Filter,
                  x best-external, a additional-path, c RIB-compressed,
    Origin codes: i - IGP, e - EGP, ? - incomplete
    RPKI validation codes: V valid, I invalid, N Not found

         Network          Next Hop            Metric LocPrf Weight Path
    *>   192.0.2.0        198.51.100.1             2              0 100 i
    ISP1# show ip route 192.0.2.0 255.255.255.0 longer-prefixes
    ! Legend omitted

    B     192.0.2.0/24 [20/2] via 198.51.100.1, 00:01:52
    ISP1#
```

Even with this basic example, the output on ISP1 reveals some key facts about how BGP works. Note that the **show ip bgp** command's *Path* column now lists ASN 100, whereas that column in R1's output listed no ASNs. (That column lists the *AS_PATH* PA, which in this case lists the enterprise's ASN.) Also, note ISP1's next-hop address for this prefix, 198.51.100.1, which is R1's IP address on the link between R1 and ISP1. By default, when a router learns a prefix with *eBGP*, like the route ISP1 is shown to learn in Example 12-5, the router uses the IP address of the eBGP neighbor as the next-hop address.

| Command | Mode and Purpose |
| --- | --- |
| network *prefix* [mask *mask*] | Directs the BGP process to add a BGP table entry for the prefix/mask if the prefix/mask exists in the IP routing table |
| ip route *prefix mask* null0 | Defines a discard route, so that packets routed by the router that use this route will be discarded by the router |

**Table 12-6** Chapter 12 EXEC Command Reference

| Command | Purpose |
| --- | --- |
| show ip bgp | Displays the BGP table |
| show ip bgp summary | Displays basic configuration for the local router, and one line of configuration and state information per BGP peer |
| show tcp summary | Lists a line of information about each TCP connection that terminates at the router |
| show ip route *prefix mask*<br>longer-prefixes | Lists a subset of IP routes, listing one line per route that exists within the address range defined by the prefix and mask |

## Part III

### Wide-Area Networks

- Chapter 13: Implementing Point-to-Point WANs
- Chapter 14: Private WANs with Ethernet and MPLS
- Chapter 15: Private WANs with Internet VPNs
- Part III Review

## Implementing Point-to-Point WANs

**This chapter covers the following exam topics:**

- **3.0 WAN Technologies**
- 3.1 Configure and verify PPP and MLPPP on WAN interfaces using local authentication

Leased-line WANs—also known as serial links—require much less thought than many other topics, at least to the depth required for the CCENT and CCNA R&S exams. That simplicity allows the Cisco exams to discuss leased lines briefly for the ICND1 exam, while using leased lines as part of larger discussions of IP routing.

This chapter finally takes the discussion of leased-line WANs deeper than has been discussed so far. This chapter briefly repeats the leased-line concepts from the ICND1 book, to lay a foundation to discuss other concepts. More important, this chapter looks at the configuration, verification, and troubleshooting steps for leased lines that use the familiar High-level Data Link Control (HDLC) data-link protocol and the Point-to-Point Protocol (PPP).

This chapter breaks the material down into three major sections. The first looks at leased-line WANs that use HDLC, by reviewing and adding details about the physical links themselves, along with HDLC (and related) configuration. The second major section discusses PPP, an alternate data-link protocol that you can use instead of HDLC, with a focus on concepts and configuration. The final major section then discusses typical root causes of serial link problems and how to find those problems.

### “Do I Know This Already?” Quiz

Take the quiz (either here, or use the PCPT software) if you want to use the score to help you decide how much time to spend on this chapter. The answers are at the bottom of the page following the quiz, and the explanations are in DVD Appendix C and in the PCPT software.

**Table 13-1** “Do I Know This Already?” Foundation Topics Section-to-Question Mapping

| Foundation Topics Section | Questions |
|---|---|
| Leased-Line WANs with HDLC | 1–2 |
| Leased-Line WANs with PPP | 3–6 |
| Troubleshooting Serial Links | 7 |

1. In the cabling for a leased line, which of the following usually connects to a four-wire line provided by a telco?
   - a. Router serial interface without internal CSU/DSU
   - b. CSU/DSU
   - c. Router serial interface with internal transceiver
   - d. Switch serial interface

2. Two routers connect with a serial link, each using its S0/0/0 interface. The link is currently working using PPP. The network engineer wants to migrate to use the Cisco-proprietary HDLC that includes a protocol type field. Which of the following commands can be used to migrate to HDLC successfully? (Choose two answers.)
   - a. encapsulation hdlc
   - b. encapsulation cisco-hdlc
   - c. no encapsulation ppp
   - d. encapsulation-type auto

3. Which of the following PPP authentication protocols authenticates a device on the other end of a link without sending any password information in clear text?
   - a. MD5
   - b. PAP
   - c. CHAP
   - d. DES

4. Two routers have no initial configuration whatsoever. They are connected in a lab using a DTE cable connected to R1 and a DCE cable connected to R2, with the DTE and DCE cables then connected to each other. The engineer wants to create a working PPP link by configuring both routers. Which of the following commands are required in the R1 configuration for the link to reach a state in which R1 can ping R2's serial IP address, assuming that the physical back-to-back link physically works? (Choose two answers.)
   - a. encapsulation ppp
   - b. no encapsulation hdlc
   - c. clock rate
   - d. ip address

5. Consider the following excerpt from the output of a show command:

   ```
   Serial0/0/1 is up, line protocol is up
     Hardware is GT96K Serial
     Internet address is 192.168.2.1/24
     MTU 1500 bytes, BW 1544 Kbit, DLY 20000 usec,
        reliability 255/255, txload 1/255, rxload 1/255
     Encapsulation PPP, LCP Open
     Open: CDPCP, IPCP, loopback not set
   ```

   Which of the following are true about this router's S0/0/1 interface? (Choose two answers.)
   - a. The interface is using HDLC.
   - b. The interface is using PPP.
   - c. The interface currently cannot pass IPv4 traffic.
   - d. The link should be able to pass PPP frames at the present time.
