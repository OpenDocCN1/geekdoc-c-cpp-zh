# Gateway Functionality

Cisco voice gateways can be either digital gateways or analog gateways. Digital gateways connect to telephone service providers through ISDN, T1, or E1 lines. Analog gateways connect to either telephone service providers or analog telephony devices. Voice ports are commonly used within gateways to provide the following connection types:

+   - Telephone to WAN
+   - Telephone to PSTN
+   - PBX-to-PBX over WAN

When implementing telephone to WAN connections, you are either supporting internal analog or VoIP phones connecting over the WAN to remote locations in your organization or another organization to which you connect. Figure 14-1 shows the concept of the telephone to WAN implementation. The VoIP phone will connect to the gateway through standard Ethernet ports, and a digital line will usually be utilized for the WAN connection. If internal analog phones are supported, they may connect to the gateway directly using FXS (foreign exchange station) ports or through an analog to VoIP conversion device of some type.

The telephone to PSTN model uses either analog or VoIP phones within the organization and connects to the PSTN instead of to a WAN link. Figure 14-2 illustrates the telephone to PSTN implementation. With the telephone to PSTN model, the internal phones communicate with the gateway using either Ethernet communications (VoIP phones) or FXS ports (analog phones). The gateway communicates with the PSTN using analog or digital interfaces. If only a few

FIGURE 14-1
Telephone to WAN implementation

![](bbox=[0.21, 0.72, 0.97, 0.82])