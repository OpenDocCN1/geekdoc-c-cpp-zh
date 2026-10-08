
Note: Many VoIP deployments now connect to the PSTN using an Internet Telephony Service Provider (ITSP) rather than a traditional TSP. In this case, the CME relays the voice call over a SIP trunk rather than an analog or digital circuit.

The CME router has now established two different "legs" of the call: one to the PSTN and the other to the Cisco IP Phone. It stands in the middle, independently handling signaling from both sides in two different formats. Unlike the first example, the CME router is now a critical piece of the ongoing RTP audio flow. If it were to fail in the middle of the call, the audio for the call would also fail.

# A Match Made in Heaven: CME and CUE

CUE is a fantastic, all-in-one call processing device, provided someone is there to answer the phone. However, just like the full-blown CUCM, there are no built-in voicemail capabilities. All that changes when CUE steps onto the stage: CUE is a voicemail system that you can install into your CME router in one of two form factors: Internal Services Module (ISM) or Service Module (SM). The ISM form factor installs internally to the CME router and uses solely flash memory for storage. The full SM form factor installs externally to the router and uses a hard disk for storage. Because of this, it can hold roughly ten times as much voicemail as the ISM form factor.

Cisco designed ISM and SM for the ISR G2 series of routers (1900, 2900, and 3900). They are upgrades from the previous Advanced Integration Modules (AIM) and Network Modules (NM), shown in Figure 2-3 and Figure 2-4, which were used in the first-generation ISR routers (1800, 2800, and 3800).

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_64_0.png)

Figure 2-3 CUE AIM

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_64_1.png)

Figure 2-4 CUE NM

Each module runs its Linux-based operating system (OS) that you can access and manage from the Cisco IOS of the CME router. Table 2-3 shows the current hardware limitations of each module type.

# Table 2-3 Cisco Unity Express Modules

| Platform | Hardware | Included Ports | Maximum Ports | Mailboxes | Storage (Hours) |
|---|---|---|---|---|---|
| Cisco 2800/3800 (ISR Generation 1) | AIM2-CUE-K9 | 6 | 6 | 65 | 14 |
| | NME-CUE | 8 | 24 | 275 | 300 |
| Cisco 2900/3900 (ISR Generation 2) | ISM-SRE-300-K9 | 2 | 10 | 100 | 60 |
| | SM-SRE-700-K9 | 4 | 32 | 300 | 600 |

The Included Ports and Maximum Ports shown in Table 2-2 represent how many concurrent sessions (essentially, how many people can retrieve or leave voicemail at the same time). You can increase the ports by purchasing licenses.

Working with the CUE module is a little bizarre at first. Although you install the CUE module into the CME router, it still runs its own independent OS. After you access it from the IOS command line, you will find yourself in a completely new OS that looks and feels like the IOS but a completely different set of commands. Most administrators use the CUE command-line access just enough to get the CUE web-based GUI running and handle all administration from there.

Despite the small size of CUE, it has some powerful features to support your IPT network:

- **Voicemail**: The core feature provided by CUE. The type of CUE module you choose determines the maximum mailboxes and storage space used for this feature (refer to Table 2-2).
- **Auto-attendant**: The automated voice everyone loves to hear! An auto-attendant might replace an organization's operator and allow dial by name, dial by extension, and some basic menu capabilities.
- **Interactive voice response (IVR) system**: CUE includes basic IVR capabilities that allow callers to move through a menu system, providing more features than the auto-attendant. For example, a user can query a corporate database for a bank account balance or the date of a last payment received.
- **Native T.37 fax processing**: CME supports the T.37 fax standard to receive and process faxes as TIFF e-mail attachments, CUE can then distribute the fax to a user's mailbox.
- **Survivable Remote Site Voicemail (SRSV)**: Allows the CUE module to act as a backup to a primary voicemail server (perhaps running the full Unity Connection) if the IP phones are not able to reach the primary voicemail server. This feature integrates with Survivable Remote Site Telephony (SRST), which allows the CME router to act as a backup to a primary call-management system (perhaps CUCM).
- **Standards-based**: All signaling between the CME router and CUE module use the SIP protocol, which is the universal standard for voice signaling.

# Understanding Cisco Unified Communications Manager

When Cisco first released CallManager 2.4, it was an application on the Microsoft NT 4.0 OS supported by the Internet Information Server (IIS) web server. You could install it on a laptop to give yourself a battery backup power supply in case of a power outage.

**Note:** Cisco does not recommend installing CallManager on a laptop to give yourself a battery power supply.

Needless to say, Cisco has come a long way as CUCM moves beyond the 8.X versions. It runs as a Linux application on certified hardware platforms and acts as the powerful call processing component of the Cisco Unified Communications solution. Think of CUCM as the "director" behind any large organization's IPT solution. It provides the core device control, call routing, permissions, features, and connectivity to outside applications. The scope of control handled by CUCM is so large, Cisco created two certifications for it in the CCNP Voice certification track (IPT1 and IPT2). In a nutshell, the importance of CUCM to Cisco VoIP is monumental. With that being said, Cisco has done a fantastic job at allowing you to manage nearly every CUCM option through a crisp, well-designed web-GUI.

# CUCM Key Features

Although CUCM supports numerous capabilities, here are some of the most important:

- **Full support for audio and video**: CUCM supports both audio and video capabilities.
- **Appliance-based**: CUCM runs as an appliance, which provides high availability.
- **Redundant server**: When most people think of a cluster, they think of multiple servers with mirrored configurations. That is not the functionality of a CUCM server. Instead, think of a CUCM cluster as multiple, individual servers with their own, unique configuration working for the common good of the IP Phones.
- **Built-in Disaster Recovery System (DRS)**: CUCM has a built-in feature for disaster recovery.
- **Virtualization support**: If you love VMware, you’ll love the VMware environment.
- **Directory service integration**: CUCM can be its own directory or it can integrate into an existing directory structure (such as Microsoft).

> Note: Cisco produces a single-server solution known as CUCM Business Edition. This single server provides CUCM, Unified Mobility, and Unity Connection up to 500 users. The catch? CUCM Business Edition does not support clustering.

# CUCM Database Replication and Interaction with IP Phones

Even though CUCM can scale to a massive size, it interacts with IP Phones in a similar manner to CME—just bigger! The first thing you’ll want to catch is that CUCM works in a cluster. The CUCM cluster relationship includes two types of communication:

- **CUCM Database Relationship**: The CUCM database includes all the "static" data of the cluster (directory nodes, route plan, calling permissions, and so on). This replicates to all the servers in the cluster.
- **CUCM Runtime Data**: just like the name sounds, the runtime data encompasses anything happening in "real time" in the CUCM cluster. For example, when a device registers with a CUCM server, it communicates to all the other servers that "owns" that IP phone.

Although the CUCM runtime data is important for functionality, it’s simply too much to all. All the servers in the CUCM cluster form TCP sessions to each other for ICCS communication (TCP ports 8002 to 8004). When, anything of interest happens (such as a phone registering, a call invitation, a disconnect, and so on), the servers inform each other of the event.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_66_0.png)
