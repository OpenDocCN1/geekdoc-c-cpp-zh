
## CCNA ICND2 200-105 Exam Updates

Over time, reader feedback allows Pearson to gauge which topics give our readers the most problems when taking the exams. To assist readers with those topics, the authors create new materials clarifying and expanding on those troublesome exam topics. As mentioned in the Introduction, the additional content about the exam is contained in a PDF on this book’s companion website, at http://www.ciscopress.com/title/9781587205798.

This appendix is intended to provide you with updated information if Cisco makes minor modifications to the exam upon which this book is based. When Cisco releases an entirely new exam, the changes are usually too extensive to provide in a simple update appendix. In those cases, you might need to consult the new edition of the book for the updated content.

This appendix attempts to fill the void that occurs with any print book. In particular, this appendix does the following:

- Mentions technical items that might not have been mentioned elsewhere in the book
- Covers new topics if Cisco adds new content to the exam over time
- Provides a way to get up-to-the-minute current information about content for the exam

### Always Get the Latest at the Book’s Product Page

You are reading the version of this appendix that was available when your book was printed. However, given that the main purpose of this appendix is to be a living, changing document, it is important that you look for the latest version online at the book’s companion website. To do so, follow these steps:

- **Step 1.** Browse to www.ciscopress.com/title/9781587205798.
- **Step 2.** Click the Updates tab.
- **Step 3.** If there is a new Appendix B document on the page, download the latest Appendix B document.

![](img/79473ea15699e01619d2aa789f5bd43b_867_0.png)

**2-way state** In OSPF, a neighbor state that implies that the router has exchanged Hellos with the neighbor and that all required parameters match.

**3G/4G Internet** An Internet access technology that uses wireless radio signals to communicate through mobile phone towers, most often used by mobile phones, tablets, and some other mobile devices.

**802.1Q** The IEEE standardized protocol for VLAN trunking.

## A

**AAA server** *See authentication, authorization, and accounting (AAA) server.*

**ABR** Area Border Router. A router using OSPF in which the router has interfaces in multiple OSPF areas.

**access interface** A LAN network design term that refers to a switch interface connected to end-user devices, configured so that it does not use VLAN trunking.

**access link (WAN)** A physical link between a service provider and its customer that provides access to the SP's network from that customer site.

**access rate** The speed at which bits are sent over an access link.

**ACI** *See Application Centric Infrastructure.*

**ACL** Access control list. A list configured on a router to control packet flow through the router, such as to prevent packets with a certain IP address from leaving a particular interface on the router.

**adjacency table** In Cisco IOS CEF, a table that keeps a copy of the outgoing data link headers that a router will then add to a packet before forwarding the packet, for the purpose of reducing the per-packet processing done by the router.

**administrative distance** In Cisco routers, a means for one router to choose between multiple routes to reach the same subnet when those routes are learned by different routing protocols. The lower the administrative distance, the more preferred the source of the routing information.

**administrative mode** *See trunking administrative mode.*

**ADSL** Asymmetric digital subscriber line. One of many DSL technologies, ADSL is designed to deliver more bandwidth downstream (from the central office to the customer site) than upstream.

**alternate port** With 802.1w RSTP, a port role in which the port acts as an alternative to a switch's root port, so that when the switch's root port fails, the alternate port can immediately take over as the root port.

**analog modem** *See modem.*

**anti-replay** Preventing a man in the middle from copying and later replying the packets sent by a legitimate user, for the purpose of appearing to be a legitimate user.

**APIC** *See* Application Policy Infrastructure Controller.

**APIC-EM** *See* Application Policy Infrastructure Controller – Enterprise Module.

**Application Centric Infrastructure (ACI)** Cisco's data center SDN solution, with the concepts of defining policies that the APIC controller then pushes to the switches in the network using the OpFlex protocol, with the partially distributed control plane in each switch building the forwarding table entries to support the policies learned from the controller. It also supports a GUI, a CLI, and APIs.

**Application Policy Infrastructure Controller (APIC)** The software that plays the role of controller, controlling the flows that the switches create to define where frames are forwarded, in a Cisco data center that uses the Application Centric Infrastructure (ACI) approach, switches, and software.

**Application Policy Infrastructure Controller – Enterprise Module (APIC-EM)** The software that plays the role of controller in an enterprise network of Cisco devices, in its first version as of the publication of this book, which leaves the distributed routing and switching control plane as is, instead acting as a management and automation platform. It provides robust APIs for network automation, and uses CLI (Telnet and SSH) plus SNMP southbound to control the existing routers and switches in an enterprise network.

**application programming interface (API)** A software mechanism that enables software components to communicate with each other.

**application signature** With Network Based Application Recognition (NBAR), the definition of a combination of matchable fields that Cisco has identified as being characteristic of a specific application, so that NBAR can be configured by the customer to match an application, while IOS then defines the particulars of that matching.

**application-specific integrated circuit (ASIC)** An integrated circuit (computer chip) designed for a specific purpose or application, often used to implement the functions of a networking device rather than running a software process as part of the device's OS that runs on a general-purpose processor.

**AR** *See* access rate.

**Area Border Router** *See* ABR.

**ARP** Address Resolution Protocol. An Internet protocol used to map an IP address to a MAC address. Defined in RFC 826.

**AS_Path** A BGP path attribute that lists the ASNs in the path (other than the ASN of the router on which the AS_Path is examined).

**ASAv** A Cisco ASA firewall software image that runs as a virtual machine rather than on Cisco hardware, intended to be used as a consumer-controlled firewall in a cloud service or in other virtualized environments.

**ASBR** Autonomous System Border Router. A router using OSPF in which the router learns routes via another source, usually another routing protocol, exchanging routes that are external to OSPF with the OSPF domain.

**ASIC** *See* application-specific integrated circuit.

**Assured Forwarding (AF)** The name of a grid of 12 DSCP values, and a matching grid of per-hop behavior as defined by DiffServ. AF defines four queuing classes, and three packet drop priorities within each queuing class. The text names of the 12 DSCP values follow a format of AFXY, where X is the queuing class, and Y is the drop priority.

**authentication** The ability to verify the identity of a user or a computer system on a computer network.

**authentication, authorization, and accounting (AAA) server** A server that holds security information and provides services related to user login, particularly authentication (is the user who they say they are), authorization (once authenticated, what do we allow the user to do), and accounting (tracking the user).

**authenticator** With IEEE 802.1x, the LAN switch that uses EAPoL to ask for the identification from the supplicant (the end-user device), and then passes the EAP messages to a AAA server to authenticate the user.

**autonomous system (AS)** An internetwork that is managed by one organization.

**Autonomous System Border Router** *See* ASBR.

**autonomous system number (ASN)** A number used by BGP to identify a routing domain, often a single enterprise or organization. As used with EIGRP, a number that identifies the routing processes on routers that are willing to exchange EIGRP routing information with each other.

**AutoQoS** In Cisco switches and routers, an IOS feature that configures a variety of QoS features with useful settings as defined by the Cisco reference design guide documents.

**autosummarization** A routing protocol feature in which a router that connects to more than one classful network advertises summarized routes for each entire classful network when sending updates out interfaces connected to other classful networks.

**autosummary** *See* autosummarization.

## B

**backbone area** In OSPFv2 and OSPFv3, the special area in a multiarea design, with all non-backbone areas needing to connect to the backbone area, area 0.

**backup designated router** An OSPF router connected to a multiaccess network that monitors the work of the designated router (DR) and takes over the work of the DR if the DR fails.

**backup port** With 802.1w RSTP, a port role in which the port acts as a backup to one of the switch's ports acting as a designated port. If the switch's designated port fails, the switch will use the backup port to immediately take over as the designated port.
