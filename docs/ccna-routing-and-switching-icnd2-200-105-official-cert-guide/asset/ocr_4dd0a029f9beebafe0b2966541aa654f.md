Now that you have heard some of the big ideas and key terms from Frame Relay, the next few topics go into more depth on the core functions within Frame Relay: virtual circuits, the LMI protocol, framing, and Frame Relay addressing.

# ## Virtual Circuits

Frame Relay provides significant advantages over simply using point-to-point leased lines. The primary advantage has to do with VCs. Consider Figure H-3, which shows a typical Frame Relay network with three sites.

![](bbox=[0.15, 0.228, 0.955, 0.52])

**Figure H-3** *Typical Frame Relay Network with Three Sites*

A VC defines a logical path between two Frame Relay DTEs. The term virtual circuit describes the concept well. It acts like a point-to-point circuit, enabling the sending of data between two endpoints over a WAN. There is no physical circuit directly between the two endpoints, so it is virtual. For example, R1 terminates two VCs—one whose other endpoint is R2, and one whose other endpoint is R3. R1 can send traffic directly to either of the other two routers by sending it over the appropriate VC.

VCs share the access link and the Frame Relay network. For example, both VCs terminating at R1 use the same access link. R1 can send one Frame Relay frame to R2, and then another frame to R3, sending both over the same physical access link.

Not only does a single customer router share its access link among many VCs, many customers share the same Frame Relay network. Originally, people with leased-line networks were reluctant to migrate to Frame Relay because they would be competing with other Frame Relay customers for the provider's capacity inside the cloud. To address these fears, Frame Relay uses a concept of a committed information rate (CIR). Each VC has a CIR, which is a guarantee by the provider that a particular VC gets at least that much bandwidth. So, you can migrate from a leased line to Frame Relay, getting a CIR of at least as much bandwidth as you previously had with your leased line.

One big advantage of Frame Relay over leased lines is that Frame Relay provides connectivity to each site, with only a single access link between each router and the Frame Relay provider. Interestingly, even with a three-site network, it's probably less expensive to use Frame Relay than to use point-to-point links because the access links tend to be relatively short, to some nearby Frame Relay provider point of presence (PoP).