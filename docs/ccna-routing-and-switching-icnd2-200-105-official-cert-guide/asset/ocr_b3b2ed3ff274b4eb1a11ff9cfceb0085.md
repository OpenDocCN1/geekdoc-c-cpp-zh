the network, similar to LANs. Unlike with LANs, you cannot send a data link layer broadcast over Frame Relay. Therefore, Frame Relay networks are called nonbroadcast multiaccess (NBMA) networks. Also, because Frame Relay is multiaccess, it requires the use of an address that identifies to which remote router each frame is addressed.

Figure H-1 outlines the basic physical topology and related terminology in a Frame Relay network.

![](bbox=[0.069, 0.241, 0.133, 0.276])

![](bbox=[0.16, 0.278, 0.852, 0.462])

**Figure H-1** *Frame Relay Components*

Figure H-1 shows the most basic components of a Frame Relay network. A leased line is installed between the router and a nearby Frame Relay switch; this link is called the *access link*. To ensure that the link is working, the device outside the Frame Relay network, called the data terminal equipment (DTE), exchanges regular messages with the Frame Relay switch. These keepalive messages, along with other messages, are defined by the Frame Relay Local Management Interface (LMI) protocol. The routers are considered DTE, and the Frame Relay switches are data communications equipment (DCE).

> **NOTE** The terms *DCE* and *DTE* have different meanings in different contexts. Here, with a Frame Relay service, the roles are as described in the previous paragraph. On a physical leased line, the DCE provides Layer 1 clocking, and the DTE receives and reacts to the DCE's clock signal. These are two different (and accepted) uses of the same two terms.

Figure H-1 shows the physical connectivity at each connection to the Frame Relay network, and Figure H-2 shows the logical, or virtual, end-to-end connectivity associated with a virtual circuit (VC).

![](bbox=[0.176, 0.822, 0.852, 0.895])

**Figure H-2** *Frame Relay PVC Concepts*

The logical communications path between each pair of DTEs is a VC. The dashed line in the figure represents a single VC; this book uses a thick dashed line style to make sure that you