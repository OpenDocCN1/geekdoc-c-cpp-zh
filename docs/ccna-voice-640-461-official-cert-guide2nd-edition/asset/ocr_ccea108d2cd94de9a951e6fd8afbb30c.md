# Example 6-18 Transforming Dialed Numbers Using num-exp

```
Voice_RTR(config)# voice-port 1/0/1
Voice_RTR(config-voiceport)# connection plar 0
Voice_RTR(config-voiceport)# exit
Voice_RTR(config)# num-exp 0 5000
```

Now, anytime the number 0 is dialed from anywhere in the organization (could be an IP phone, FXS port, and so on), the voice router automatically transforms it to 5000 and then searches for a dial peer allowing it to reach the number 5000.

Note: The router applies the num-exp command the instant it receives a dialed number, even before it attempts to match an inbound dial.

# Practical Scenario 3: Specific POTS Lines for Emergency Calls

As organizations move more to VoIP connections, they are finding cost-saving benefits by eliminating traditional telephony connections at remote offices in favor of centralizing all PSTN calls (and toll charges) at a central site. Figure 6-14 illustrates this type of net-work design.

This type of call allows an organization to get higher call volume from a single location, which typically allows the organization to negotiate cheaper long-distance routes with its PSTN carrier.

Note: Some countries restrict businesses from forwarding PSTN calls over the IP WAN. You should always check with the local government regulations before you do this. Frankly, the United States is not one of those countries.

Although the centralization of PSTN calls offers significant cost savings, the remote sites need to keep at least one local PSTN connection for emergency calling. This is because PSTN carriers provide location information to emergency service providers based on the PSTN connection. If emergency calls from the remote offices were to traverse the IP WAN and leave the PSTN connection at the central site, the emergency service provider would receive location information for the central site.

Depending on the size of the remote office, you can typically dedicate one or two analog FXO ports for emergency calls. The configuration in Example 6-19 configures the necessary dial peers for dual FXO ports connected to the PSTN. This assumes the FXO ports are 1/0/0 and 1/0/1.

# Example 6-19 Dynamic WAN to PSTN Failover Implementation

```
REMOTE_RTR(config)# dial-peer voice 10 pots
REMOTE_RTR(config-dial-peer)# destination-pattern 911
REMOTE_RTR(config-dial-peer)# port 1/0/0
REMOTE_RTR(config-dial-peer)# no digit-strip
REMOTE_RTR(config-dial-peer)# exit
```