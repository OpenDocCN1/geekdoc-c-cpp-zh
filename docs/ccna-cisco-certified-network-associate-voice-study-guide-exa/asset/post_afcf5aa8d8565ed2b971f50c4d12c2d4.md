
**TABLE 9-1** Cisco Call Processing Agents Comparison

| Call Processing Agent | Phones Supported | Platform |
| --- | --- | --- |
| Cisco Unified CallManager Express (CME) | Up to 250 | Integrated Services Routers (ISRs) |
| Cisco Unified Communications Manager (CUCM) | Up to 30,000 phones per cluster, with multiple clusters supported | Media Convergence Servers |
| Cisco Unified Communications Manager Business Edition | Up to 500 phones | Media Convergence Servers |
| Cisco Smart Business Communications System (SBCS) – UC500 series | Up to 48 phones | Specialized router in the UC500 series |

## Messaging

To provide voice mail, e-mail, calendaring, and faxing for your VoIP users, Cisco provides the Unity series of solutions. Three levels are available within the Unity products. The levels are Cisco Unity Express, Cisco Unity Connection, and Cisco Unity.

### Cisco Unity Express

Cisco Unity Express provides support for up to 275 mailboxes and integrates voice mail, faxing, and interactive voice response solutions. Unity Express is an add-on for select Cisco ISRs. It comes with either flash memory or a hard drive for storage of messaging data. The flash version comes in the Advanced Integration Module (AIM) form factor. The Network Module (NM) form factor is used for the hard drive models.

The Unity Express module (both AIM and NM) is configured through a Linux-based interface that runs on the router. When you enter the Unity Express configuration mode, you will no longer be working with a traditional IOS command line, but with the Linux-based command line used for configuration of the Unity Express.

> **Exam Watch**
>
> Remember that the Unity Express modules use a Linux-based command line that runs on the IOS router, not the built-in IOS operating system command line.

The following features are provided by Cisco Unity Express:

- Voice messaging and greeting services for better customer service and employee communications
- Time-card data management with TimeCardView
- Telephone prompts and a web-based interface for fast, convenient voice mail, auto attendant, and interactive voice response (IVR) administration
- Ability to view, sort, search, and play back voice messages using a Cisco Unified IP Phone display or your e-mail client
- Scalability of up to 24 concurrent voice mail or auto attendant calls and 275 mailboxes

Cisco Unity Express is aimed at the distributed enterprise, branch office, or SMB (small- and medium-size business) market. The AIM version of Unity Express supports only 50 mailboxes due to the limited memory available on flash.

### Cisco Unity Connection

The next level is the Cisco Unity Connection. Unity Connection supports up to 20,000 mailboxes per server. Unity Connection can be used as an add-on to a CUCM Business Edition installation for up to 500 users. Larger organizations can interconnect multiple Unity Connection, Unity Express, or Unity messaging products to support thousands of users.

Cisco Unity Connection provides the following features:

- Voice messaging with advanced capabilities
- Speech-enabled messaging for interface navigation and message management
- Message access from the computer desktop through web interfaces, IMAP e-mail clients, or visual voice mail on the Cisco IP Phones that support the visual voice mail feature
- Interconnectivity with Cisco Unity so that the two systems can work together for seamless communications

Cisco Unity Connection is aimed at the enterprise, commercial, and SMB markets.

### Cisco Unity

Cisco Unity, interestingly aimed at only the enterprise and commercial markets according to Cisco literature, supports up to 15,000 mailboxes per server compared with Cisco Unity Connection’s 20,000. However, Cisco Unity can scale to 250,000 total network users with multiple servers, while Cisco Unity Connection can only scale to 100,000 total network users.

Cisco Unity comes in different versions for integration with different e-mail server products. For example, Cisco Unity for Microsoft Exchange works with Microsoft’s e-mail server, and Cisco Unity for Lotus Domino works with IBM’s e-mail server. Cisco Unity and Cisco Unity Connection both operate on dedicated servers or server appliances, while Cisco Unity Express runs on ISRs.

### On the Job

> Always check the Cisco web site for the latest information. Many early books indicate that lower numbers of mailboxes are supported than, for example, the 15,000 referenced here. However, the information here is based on Cisco’s documentation for version 8 of the Unity products at the time this book was written.

## Auto Attendants

The interactive voice response (IVR) feature of Cisco’s VoIP products allows the device or server to communicate with the calling user by playing recorded messages. For example, when you call customer service for any company, you often receive recorded messages telling you to press 1 for a specific service, press 2 for another, and so forth. These recorded messages are driven by an IVR.

An auto attendant usually uses the features of the IVR to communicate with the user and to allow for self-direction on the voice network. In other words, the user can connect with an individual within your organization without requiring the aid of an operator. You may support Auto Attendant functions for direct dialing to extensions or for access to departments. For example, the caller may press 3 for the Accounting department, which could route him to a group of potential endpoints where the first available phone rings, and an accountant would answer to assist the caller.

## Contact Center

Larger companies often have a call center or contact center that acts as the incoming hub for all calls. One or more operators or receptionists may answer these incoming calls and direct them to the appropriate departments or endpoints. To operate such a contact center, software must be implemented that supports call distribution, queue management, and call reporting.

Cisco’s Unified Contact Center (UCC) provides the features required of a contact center. These features include:

- **Automatic call distribution (ACD)** — The ACD feature allows calls to be distributed to the appropriate user or group of users. The ACD will often integrate with an IVR solution as well.
- **Computer telephony integration (CTI)** — CTI can also be used to provide information about the caller on the computer screen of the answering user. This information may include the phone number and name of the caller if Caller ID data is provided.
- **Collaboration features** — The Cisco UCC also provides collaboration features such as chat, e-mail, and web collaboration.

Cisco UCC comes in both Express and Enterprise editions. The UCC Express Edition supports up to 300 agents. Larger call centers will need the UCC Enterprise Edition.

## Applications in the UC Environment

CUCM and CME can provide several features that enhance the user’s experience when using the VoIP network. The most important of these features are mobility, presence, and TelePresence.

### Mobility

Cisco Unified Mobility, or simply “mobility,” allows users to redirect calls from CUCM to as many as four different client devices like cellular phones or wired and wireless IP phones. This feature is also known as Single Number Reach or Single Business Number Reach. Solutions available with Cisco Unified Mobility include:

- **Device Mobility** — The Cisco Mobile Connect services, which are part of Cisco Unified Mobility, allow mobile workers to continue a call on the IP desk phone that began on another phone (such as a cellular phone) or vice versa.
- **Mobile Voice Access** — Calls can be placed from anywhere as if the user were connected directly to the enterprise home office. The user dials into the Cisco Mobile Voice Access line from a cellular or land-line phone and then places calls across the VoIP network.
- **Web-based Administration** — Users can access their
