# Foundation Topics

# Implementing IP Phones in CUCM

The implementation of IP Phones is remarkably simple, considering the myriad of services, protocols, and processes going on in the background to make the system work well. This section reviews these "hidden" processes and details some of the administrative tasks required to easily and reliably run IP Phones in CUCM.

Special Functions and Services Used by IP Phones

A variety of standards-based and proprietary protocols and services support IP Phones in CUCM. In no particular order, they include the following:

+   - Network Time Protocol (NTP)
- Cisco Discovery Protocol (CDP)
- Dynamic Host Configuration Protocol (DHCP)
- Power over Ethernet (PoE)
- Trivial File Transfer Protocol (TFTP)
- Domain Name System (DNS)

The next section describes each of these services, how IP Phones use them, and how to configure them in CUCM (or other systems as appropriate).

# NTP

NTP is an IP standard that provides network-based time synchronization. There are many reasons to use NTP beyond the convenience and consistency of having the same time on all devices. Call Detail Records (CDR) and Call Management Records (CMR) are time stamped, as are log files. Parsing sequential events across multiple platforms is much simpler and easier to understand if the relative time is exactly the same on all those devices. Functions and features can also be time (calendar) based, too, so time synchronization is important for those functions to operate properly.

In a typical NTP implementation, a corporate router synchronizes its clock with an Internet time server (such as a NIST atomic clock or a GPS satellite clock). Other devices in the corporate network then sync to the router.

The Cisco Unified Communications Manager (CUCM) Publisher is one such device; during installation, CUCM asks for the IP address of an NTP server. (Alternatively, it can use its internal clock, which is not recommended because of its inaccuracy compared to NTP). The Subscribers then sync their clocks to the Publisher, and the IP Phones get their time from their Subscribers via Skinny Client Control Protocol (SCCP) messages. Session Initiation Protocol (SIP) phones need an NTP reference (detailed later), but in one of them, they can get the time from the time in the SIP OK from the absence of the Subscriber server.