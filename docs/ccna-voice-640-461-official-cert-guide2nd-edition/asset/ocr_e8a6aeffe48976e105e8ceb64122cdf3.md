Note: Many VoIP deployments now connect to the PSTN using an Internet Telephony Service Provider (ITSP) rather than a traditional TSP. In this case, the CME relays the voice call over a SIP trunk rather than an analog or digital circuit.

The CME router has now established two different "legs" of the call: one to the PSTN and the other to the Cisco IP Phone. It stands in the middle, independently handling signaling from both sides in two different formats. Unlike the first example, the CME router is now a critical piece of the ongoing RTP audio flow. If it were to fail in the middle of the call, the audio for the call would also fail.

# A Match Made in Heaven: CME and CUE

CUE is a fantastic, all-in-one call processing device, provided someone is there to answer the phone. However, just like the full-blown CUCM, there are no built-in voicemail capabilities. All that changes when CUE steps onto the stage: CUE is a voicemail system that you can install into your CME router in one of two form factors: Internal Services Module (ISM) or Service Module (SM). The ISM form factor installs internally to the CME router and uses solely flash memory for storage. The full SM form factor installs externally to the router and uses a hard disk for storage. Because of this, it can hold roughly ten times as much voicemail as the ISM form factor.

Cisco designed ISM and SM for the ISR G2 series of routers (1900, 2900, and 3900). They are upgrades from the previous Advanced Integration Modules (AIM) and Network Modules (NM), shown in Figure 2-3 and Figure 2-4, which were used in the first-generation ISR routers (1800, 2800, and 3800).

![](bbox=[0.105, 0.584, 0.843, 0.715])

Figure 2-3 CUE AIM

![](bbox=[0.105, 0.786, 0.543, 0.917])

Figure 2-4 CUE NM