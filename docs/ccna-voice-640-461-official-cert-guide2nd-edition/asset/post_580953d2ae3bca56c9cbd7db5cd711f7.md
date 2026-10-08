
![](img/e4ad7862dc47b4e5de0cde3b4550ad65_410_0.png)

# Figure 14-1 CUPC in Deskphone Mode

- Softphone mode: When the IP phone is not available or the user is away from his desk, CUPC activates the associated softphone based on the Cisco Unified Client Services Framework (CSF), which registers the softphone with CUCM as a SIP device (see Figure 14-2). The CUCM administrator must create the CSF device in order to enable this functionality.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_410_1.png)

# Figure 14-2 CUPC in Softphone Mode

# Enterprise Instant Messaging

CUPC provides TLS-secured Chat and Group Chat capability. Ad-Hoc Group Chat sessions are stored in memory on the CUPC server. The Persistent Chat feature enables group chat rooms where the conversation persists even when all participants have left the chat session. If Persistent Chat is enabled, it requires an external database to store the chat rooms and conversations. Offline IM chat messages to be sent to users who are currently offline; these messages are stored in the local IDS database on the CUPC server.

### The Jabber XCP message routing system

The Jabber XCP message routing system has been modified in the CUPC implementation to improve functionality when users are available on multiple devices. Messages are

> Topic

routed to all the non-negative priority devices the user is logged into, instead of routing only to the highest-priority device (Non-negative means devices that are not explicitly blocked from receiving messages). CUPS delivers messages to all the logged-in devices for a user (this behavior is called IM Forking). When the user replies on a particular device, subsequent messages are sent only to the device used for the reply. Backward compatibility for SIP-only Presence clients (such as CUPC 7x) is provided via an IM gateway.

# Voice Calls

CUPSC supports voice calls in deskphone mode or softphone mode. Voice encryption using Real-Time Protocol (SRP) is supported. Survivable Remote Telephony (SRST) is supported in softphone mode with appropriate CUCM/CSF configuration. CUPC supports the following codecs in softphone mode:

- G.711 a-law, mu-law
- G.722 Wideband
- G.729A, G.729B
- iBC (Internet Low Bandwidth Codec)
- iASAC (Internet Speech Audio Codec)

CDEC support in deskphone mode depends on the IP phone model.

# Voice Calls

CUPSC supports voice calling in either deskphone or softphone mode. In deskphone mode, CUPSC uses Cisco Audio Session Tunnel (CAST) and Cisco Discovery Protocol (CDP) for communication between the IP phone and the computer running CUPC. The desk phone must be enabled for voice support in CUCM. SIP desk phones are not supported by CAST.

In softphone mode, CUPSC uses the CSF device configured on CUCM for video calls. CSF devices are video-enabled by default.

Video conferencing is supported, using a video-conference bridge accessible by the Media Resource Group List (MRGL) assigned to the IP phone or CSF device.

# Integration Support

CUPSC can integrate with many Cisco Unified Communications applications, providing a wide range of rich features. CUPC can provide visual voicemail when integrated with Cisco Unity or Unity Connection. Users can control their mailboxes and listen to, send, and delete messages using CUPC.

Click-to-call functionality is supported by CUPC and other applications, such as Microsoft Outlook, Word, and Excel. Presence indicators for contacts can also be viewed in Outlook. If Cisco Unified MeetingPlace is integrated in the system, a call in CUPC can be easily escalated to a conference.

# Cisco System Requirements

Refer to the Cisco documentation at www.cisco.com/en/US/products/ps6844/index.html for current system requirements for Windows and Macintosh operating systems (OS).

# Cisco Unified Client Services Framework

The Cisco Unified Client Services Framework (CSF) provides the foundation of all Unified Communications client software. It is part of CUPC, but it also extends the functionality of Microsoft Outlook and WebEx Connect. The core functionality of CSF is video and video, secure communication with text (IM) servers such as CUPC, CSF with CUCM, provides audio and video call control and advanced features, such as voicemail support.

Only one CSF can be installed at one time on a client PC; for example, CUPC and Cisco Unified Communications Integration for Microsoft Office Communicator cannot co-reside on the same client computer.

# Cisco Unified Communications Manager IP Phone Service

The Cisco Unified Communications Manager IP Phone (CCMCIP) Service was originally used to provide authentication, directory services, and help for end users. It has been adapted for use by CUPC and CSF clients to retrieve a list of devices on which the user can be reached when they log in. Figure 14-3 illustrates CUPC's use of the CCMCIP service.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_412_0.png)

Figure 14-3 CCMCIP Interaction

# Cisco IP Phone Messenger

Cisco IP Phone Messenger (IPPM) is an IP phone service that allows a user to build a contact list and see the Presence status of those contacts, all from their IP desk phone. The service also allows users to read and clear IM messages from others, respond to the sender by calling them, or send preconfigured text messages directly from the phone.(The text of these messages can be customized by the CUCM administrator.) Users can also change their Presence status using the IP phone.

The background components of IPPM include XML-over-HTTP signaling between the IP phone running the CUPS, and XMPP between CUPS and CUPC on the user's workstation. SIP is used for communication with SIP proxy or registrar servers. Figure 14-4 illustrates protocol interactions using IPPM.

| Cisco Unified Presence | XML over HTTP | XMPP |
| :--- | :--- | :--- |
| Cisco Unified IP Phone | | Cisco Unified Personal Communicator | |

**Figure 14-4** Cisco IPPM Protocol Interaction

# Describe Cisco Unified Presence Architecture

> Key Topic

CUPS is a standards-based application that uses several protocols to provide functionality and feature richness; and XMPP to provide generic Presence and federation functionality

- SIP, SIMPLE, and XMPP
- Simple Object Access Protocol (SOAP) to access the CUCM database via Cisco Unified Communications System XML and CUPC configuration profiles
- Computer telephone interface Quick T Binary Encoding (CTIQBE) for CTI integration for remote control with Microsoft Office Communicator
- HTTP to provide IP Phone Messenger (IPPM) on Cisco IP phones

The components of CUPS are as follows:

- Jabber XCP: Provides Presence, IM, contacts listing, message and call routing, and presence and federation.
- Rich Presence service: Manages Presence state gathering and Presence-enabled routing.
- Group chat storage: Ad/ Hoc group chats are normally stored in memory on the CUPS server; Persistent Chat and message archiving require an external database.

# Integration with Microsoft Office Communications Server

CUPS interoperates with Microsoft Live Communications Server 2005 or Microsoft Office Server 2007 using SIP. The Microsoft Office Communicator client and associated IP phone interoperate to provide click-to-dial, phone control, and Presence capability.

# Integration with LDAP

CUPS can be integrated with Lightweight Directory Access Protocol (LDAP) (including Microsoft Active Directory), allowing users to log in with their LDAP credentials and synchronize their Presence status with their Outlook/Exchange calendar. The LDAP directory can be searched from the CUPC interface. CUPS can communicate with Exchange using Outlook Web Access (a Web Distributed Authoring and Versioning interface provided by Exchange). The CUPS database is synchronized with CUCM, in turn synchronize its database with LDAP. CUPS can redirect authentication to LDAP, providing a single sign-on experience. Figure 14-5 shows CUPS integration with LDAP.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_414_0.png)

# Figure 14-5 CUPS Integration with LDAP

# Integration with Cisco UUC Connection

CUPS integration with CUC provides the user with the ability to sort, view, listen to, and delete voicemail messages, and call the sender of voicemail messages, all from the CUPC interface. Presence information for the sender is displayed, allowing the user to select how to communicate with the sender or escalate to a call, message, or conference. Interaction with the CUC mailbox is via Internet Message Access Protocol (IMAP) and requires a voicemail profile to be configured on the CUPS server. Figure 14-6 illustrates CUPS interaction-with CUC.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_414_1.png)

# Figure 14-6 CUPS Integration with CUC

# Integration with Conferencing Resources

CUPS uses WebEx or MeetingPlace for its conferencing capability. The use of WebEx requires a local Meeting Center server. Communication with conferencing server is via Macromedia Flash with HTTP or HTTPS for transport. Figure 14-7 shows CUPS integration-with conferencing resources.

# Integration with Calendar Resources

CUPS can integrate with Microsoft Exchange 2003 or 2007 (Active Directory 2003 or 2008 is required) to provide access to calendar status (Free/Busy/Out of Office) and map that status to a Presence status (Available, Busy, Away). A special Exchange account (with
