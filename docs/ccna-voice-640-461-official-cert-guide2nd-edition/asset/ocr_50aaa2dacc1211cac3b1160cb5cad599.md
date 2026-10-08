integrates with Survivable Remote Site Telephony (SRST), which allows the CME router to act as a backup to a primary call-management system (perhaps CUCM).

+   * Standards-based: All signaling between the CME router and CUE module use the SIP protocol, which is the universal standard for voice signaling.

# Understanding Cisco Unified Communications Manager

When Cisco first released CallManager 2.4, it as an application on the Microsoft NT 4.0 OS supported by the Internet Information Server (IIS) web server. You could install it on a laptop to give yourself a battery backup power supply in case of a power outage.

**Note:** Cisco does not recommend installing CallManager on a laptop to give yourself a battery power supply.

Needless to say, Cisco has come a long way as CUCM moves beyond the 8.X versions and. It runs as a Linux application on certified hardware platforms and acts as the powerful call processing component of the Cisco Unified Communications solution. Think of CUCM as the "director" behind any large organization's IPT solution. It provides the core device control, call routing, permissions, features, and connectivity to outside applications. The scope of control handled by CUCM is so large, Cisco created two certifications for it in the CCNP Voice certification track (IPT1 and IPT2). In a nutshell, the importance of CUCM to Cisco VoIP is monumental. With that being said, Cisco has done a fantastic job at allowing you to manage nearly every CUCM option through a crisp, well-designed web-GUI.

# CUCM Key Features

Although CUCM supports numerous capabilities, here are some of the most important:

+   * Full support for audio and video telephony: The core feature provided by CUCM. In the way CME acts as the director of a small organization, CUCM supports audio and video calls for midsize to enterprise class corporations.

+   * Appliance-based operation: Modern CUCM versions run as an appliance, which means the underlying operating system is hardened (secured) and inaccessible.

+   * Redundant server cluster: As the saying goes, "One is one, two is one." CUCM supports redundant servers configured in a cluster relationship. The clustering capability replicates both database information (containing static data such as directory numbers and route plans) and real-time information (containing dynamic data, such as active calls). CUCM can scale up to 30,000 IP phones (SCCP or SIP in insecure mode) or 27,000 IP phones (SCCP or SIP in secure mode).

+   * Intercluster and voice gateway control and communication: Even though a CUCM cluster has a limit of 30,000 IP phones, you can create many clusters as you like (with up to 30,00 IP phones each) and connect them using intercluster trunk connections. In addition to using Intercluster trunk links you can call outside of your

![](bbox=[0.878, 0.626, 0.942, 0.663])