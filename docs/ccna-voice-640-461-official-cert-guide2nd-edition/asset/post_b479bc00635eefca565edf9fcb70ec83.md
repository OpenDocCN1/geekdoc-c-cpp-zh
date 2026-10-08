
# Foundation Topics

## Implementing IP Phones in CUCM

The implementation of IP Phones is remarkably simple, considering the myriad of services, protocols, and processes going on in the background to make the system work well. This section reviews these "hidden" processes and details some of the administrative tasks required to easily and reliably run IP Phones in CUCM.

### Special Functions and Services Used by IP Phones

A variety of standards-based and proprietary protocols and services support IP Phones in CUCM. In no particular order, they include the following:

- Network Time Protocol (NTP)
- Cisco Discovery Protocol (CDP)
- Dynamic Host Configuration Protocol (DHCP)
- Power over Ethernet (PoE)
- Trivial File Transfer Protocol (TFTP)
- Domain Name System (DNS)

The next section describes each of these services, how IP Phones use them, and how to configure them in CUCM (or other systems as appropriate).

## NTP

NTP is an IP standard that provides network-based time synchronization. There are many reasons to use NTP beyond the convenience and consistency of having the same time on all devices. Call Detail Records (CDR) and Call Management Records (CMR) are time stamped, as are log files. Parsing sequential events across multiple platforms is much simpler and easier to understand if the relative time is exactly the same on all those devices. Functions and features can also be time (calendar) based, too, so time synchronization is important for those functions to operate properly.

In a typical NTP implementation, a corporate router synchronizes its clock with an Internet time server (such as a NIST atomic clock or a GPS satellite clock). Other devices in the corporate network then sync to the router.

The Cisco Unified Communications Manager (CUCM) Publisher is one such device; during installation, CUCM asks for the IP address of an NTP server. (Alternatively, it can use its internal clock, which is not recommended because of its inaccuracy compared to NTP). The Subscribers then sync their clocks to the Publisher, and the IP Phones get their time from their Subscribers via Skinny Client Control Protocol (SCCP) messages. Session Initiation Protocol (SIP) phones need an NTP reference (detailed later), but in one of them, they can get the time from the time in the SIP OK from the absence of the Subscriber server.

## CDP

CDP is a Cisco-proprietary Layer 2 protocol that provides network mapping information to directly connected Cisco devices. (You learned about CDP in your CCNA studies, so we do not detail it.) Cisco IP Phones generate CDP messages and use the voice VLAN ID from the Cisco switch to which they are connected. The IP Phone tags the voice frames it is transmitting with that VLAN ID in the 802.1Q/P frame header.

## DHCP

DHCP is a widely used IP standard that can provide the following information to IP Phones:

- IP Address
- Subnet Mask
- Default Gateway
- DNS Server(s)
- TFTP Server(s)

Although it is possible to statically configure IP Phones with all information, it would be time-consuming and error-prone. DHCP is faster, more scalable, and a widely accepted practice. DHCP can be provided by any DHCP server (because most deployments already have one), a local router, or by CUCM itself, although this is not generally recommended, particularly for larger deployments. Later sections review the configuration of DHCP services in CUCM and router IOS.

## PoE

PoE is a standards-based feature that delivers DC power over Ethernet cabling. IP Phones can use this feature, and doing so means less cabling to clutter the desk, no more power supplies for phones, and potential cost savings. PoE is generally assumed to be provided by the switch that the phones connect to, but it may also be provided by a powered patch panel or inline power injector.

## TFTP

TFTP is a critical service for IP Phones. Phones use TFTP to download their config files, firmware, and other data. Without TFTP, the phones simply do not function properly. When you make a configuration change to a device, CUCM creates or modifies a config file for the device and uploads it to the TFTP server(s). TFTP services must be provided by one (or more in larger deployments) of the CUCM services in the cluster; a generic TFTP server will not have the integrated capability that a CUCM TFTP server does and will not fulfill the role.

## DNS

DNS provides hostname-to-IP address resolution. DNS services are not critical to IP Phones. In, in most deployments, it is recommended to eliminate DNS reliance from the IP Phones [see Chapter 10, "Understanding CUCM Dial-Phone Elements and Interactions"]. In some circumstances, it is desirable. A DNS server must be external to the CUCM cluster; DNS is not a service

## IP Phone Registration Process

The steps each phone goes through as it registers and becomes operational are more complex than you might think. The following section reviews these steps:

1. The phone obtains power (PoE or AC adapter),
2. The phone loads its locally stored firmware image.
3. The phone learns the Voice VLAN ID via CDP from the switch.
4. The phone uses DHCP to learn its IP address, subnet mask, default gateway, and TFTP server. (Other items may be learned also.)
5. The phone contacts the TFTP server and requests its configuration file. (Each phone has a customized configuration file name SEP<mac address>.cnf created by CUCM and uploaded to TFTP when the administrator creates or modifies the phone.)
6. The phone registers with the primary CUCM server listed in its configuration file. CUCM then sends the softkey template to the phone using SCCP messages.

> Note: What is in SEP<mac address>.cnf file?
> The file contains a list of CUCM server, in order, that the phone should register with. It lists the TCP ports it should use for SCCP communication. It also lists the firmware version for device model and the service URLs that device should be using. The CUCM server sends configurations, such as DNs, softkeys, and speed dials, via SCCP messages in the last phase of registration.

## SIP Registration Process

SIP phones use a different set of steps to achieve the same goal. Steps 1 to 4 are the same as SCCP phones.

1. The phone contacts the TFTP server and requests the Certificate Trust file (only if the cluster is secured).
2. The phone contacts the TFTP server and requests its SEP<mac address>.cnf configuration file.
3. The phone downloads the SIP Dial Rules (if any) configured for that phone.
4. The phone registers with the primary CUCM server listed in its configuration file.
5. The phone downloads the appropriate localization files from TFTP.
6. The phone downloads softkey configurations from TFTP.
7. The phone downloads custom ringtones (if any) from TFTP.

## Preparing CUCM to Support Phones

Before we add phones, a certain amount of work should be done on the CUCM servers. This setup work makes adding phones easier, more consistent, and more scalable, assuming that we follow our design plan.

## Chapter 9. Managing Endpoints and Users in CUCM

The tasks we review in this section are as follows:

- Configure and Verify Network Services: Set up NTP, DHCP, and TFTP.
- Configure Enterprise Parameters: Modify cluster-wide default settings.
- Configure Service Parameters: Tune activation settings and behavior.

### Service Activation

Many required services are deactivated by default on CUCM. Using the Unified Serviceability admin page, you must activate the one you need. For our purposes, we activate the Cisco CallManager, Cisco TFTP, and Cisco DHCP monitor services. Figure 9-1 shows the Unified Serviceability Activation page with those services activated.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_270_0.png)

Figure 9-1 Activating Required Services

### DHCP Server Configuration

CUCM includes a basic DHCP server capability. It is intended to support only IP Phones, and not many of them: only up to 1,000 phones (this is the maximum recommended due to heavy CPU load). There is no native capability for DHCP server redundancy and only one DHCP server is supported per cluster, typically running on the Publisher. Multisubnets (scopes) can be configured on the server.
