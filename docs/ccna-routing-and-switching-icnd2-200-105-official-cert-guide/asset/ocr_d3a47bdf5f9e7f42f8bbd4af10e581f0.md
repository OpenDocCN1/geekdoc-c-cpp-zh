useful PPP features, like its different control protocols, as well as PPP authentication like CHAP. However, the PPP protocol is transported inside Ethernet frames out Ethernet interfaces.

The Cisco R&S and ICND2 200-105 exam topics list PPPoE Client functions as a topic to be covered for not only concepts, but also configuration, verification, and troubleshooting. This last major section of the chapter mirrors those verbs from the exam topics, with four subheadings, one each on PPPOE concepts, configuration, verification, and then troubleshooting.

# PPPoE Concepts

PPP was originally used on serial links, which includes those links created with dial-up analog and ISDN modems. For instance, the link from a dial user to an ISP, using analog modems, likely uses PPP today, and has for a long time. Figure 15-22 shows a basic representation of that analog dial connection with a modem that uses PPP.

![](bbox=[0.157, 0.369, 0.824, 0.492])

**Figure 15-22** *PPP Frames Between Routers over a Dial Connection to an ISP*

ISPs used PPP as the data link protocol for a couple of reasons. First, PPP supports a way to assign IP addresses to the other end of the PPP link. ISPs can use PPP to assign each customer one public IPv4 address to use. But more important for this discussion is that PPP supports CHAP, and ISPs often want to use CHAP to authenticate customers. Then, when using CHAP to authenticate, ISPs could check accounting records to determine whether the customer’s bill was paid before letting the customer connect to the Internet.

Now, think back a bit to the history of some of these Internet access technologies. ISPs in the 1990s had mostly dial customers using analog modems and PPP. Even into the 2000s, ISPs still had analog dial customers using PPP. However, by the early 2000s, DSL was becoming more common in the market, and DSL is a natural replacement for analog dial.

So, telcos and ISPs liked analog dial with PPP, but they wanted to move customers to the faster DSL...and they still wanted to use PPP! However, the DSL connect often connects a customer device (PC or router) with an Ethernet link to a DSL modem, which then connects to the phone line (see earlier Figure 15-2). That Ethernet interface on the customer PC or router only supported Ethernet data link protocols, and not PPP.

The solution was to create a new RFC that defined how to send PPP frames over Ethernet, encapsulated in an Ethernet frame, with the protocol called PPP over Ethernet. PPPoE basically creates a tunnel through the DSL connection for the purpose of sending PPP frames between the customer router and the ISP router, as shown in Figure 15-23.