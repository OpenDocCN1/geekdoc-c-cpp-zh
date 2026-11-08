+   7. ☑ C is correct. Address hiding ensures that the UBE is the only point of signaling and media entry or exit in all scenarios.
+   
+      ☒ A, B, and D are incorrect. Address hiding does not make it more difficult to hack into the network, and it does not make it easier to monitor network traffic. Additionally, the UBE is the only point of signaling and media ingress and egress for the network, not the CME.

# **642-436: Configure IP-to-IP Gateway to Provide Protocol and Media Interworking**

+   8. ☑ B is correct. The proper command for SIP-to-SIP implementation is the allowed-connections sip to sip command.
+   
+      ☒ A, C, and D are incorrect. You cannot simply indicate allowed-connections sip and implement SIP-to-SIP. You should not include hyphens between the sip to sip clause in the allowed-connections command. No such option as sip only exists for the allowed-connections command.

+   9. ☑ C is correct. The media flow-around command should be used. This command indicates that the media (RTP stream) should not be terminated and reoriginated by the UBE.
+   
+      ☒ A, B, and D are incorrect. The media flow-through command indicates that the UBE should terminate and reoriginate the RTP media streams. The media passthrough and RTP passthrough commands are not valid IOS commands.

# **642-436: Configure IP-to-IP Gateway to Provide Call Admission Control**

+   10. ☑ B is correct. The max-conn command is used to limit the number of connections that can concurrently pass through a dial peer. For example, max-conn 12 would limit the dial peer to 12 concurrent connections.
+   
+       ☒ A, B, and C are incorrect. limit-conn, upper-conn, and conn-limit are invalid IOS commands within the dial-peer configuration mode.

+   11. ☑ B is correct. Measurement-based CAC sends packets onto the WAN in order to measure the performance of the WAN. The CAC is then dynamically configured based on the results.
+   
+       ☒ A, C, and D are incorrect. Local CAC uses simple connection limits or is bound by the literal input source (such as a single POTS line). Resource-based CAC uses gatekeepers and RSVP. Gatekeeper CAC is not a Cisco term.

+   12. ☑ A and C are correct. Resource-based CAC requires both a gatekeeper and the RSVP protocol support on the endpoints and the gateways.
+   
+       ☒ B and D are incorrect. A SIP proxy is not required and DiffServe is not used.