# ## System Parameters

On the System tab, you can configure the regional settings, which impact call tones, phone languages, date and time format, and the voice mail language. You may also configure system-wide speed-dial settings here.

# ## Network Parameters

The configurable network parameters include the IP information for the UC500 device and the VLAN information. Much like SOHO routers (such as Linksys and D-Link devices), the UC500 series offers simple configuration of DHCP servers and the IP address of the call manager (the CME in the Cisco world). The following parameters can be configured on the Network tab of the Devices dialog box:

+   - **VLAN Number** This can be a number from 1 to 1001. This is the VLAN that will be configured as the voice VLAN.
+   - **DHCP IP Address Pool** This defines the range of addresses to be configured automatically for the clients. Supporting fields include the Subnet Mask, Exclude Address From, and To fields. The DHCP IP Address Pool field will contain the subnet identifier, for example, 192.168.1.0. The Subnet Mask field will contain the appropriate mask for the subnet identifier, for example, 255.255.255.0. The Exclude Address From and To fields will include the beginning and ending addresses that define the range that should not be given out by the DHCP server, such as 192.168.1.50 to 192.168.1.59.
+   - **CME IP Address** This is the IP address of the Communications Manager Express (CME) call manager server. The supporting field is the Subnet Mask field used to identify the network on which the CME server resides.

# ## Auto Attendant and Voice Mail

Several fields can be configured on the AA & Voicemail tab. The sections to be configured include Auto Attendant, Script Parameters, and Voicemail. In the Auto Attendant section, you can configure the phone extension of the Auto Attendant service. This is usually the main extension phone number for the organization. You can also configure the outside number (the PSTN number) used to reach the Auto Attendant. Finally, you can use the default AA script, or select a custom script you've developed.