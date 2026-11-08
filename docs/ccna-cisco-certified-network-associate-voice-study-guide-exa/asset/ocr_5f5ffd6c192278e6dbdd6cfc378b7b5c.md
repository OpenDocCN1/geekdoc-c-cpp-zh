# SELF TEST ANSWERS

# 642-436: Describe the IP-to-IP Gateway Features and Functionality

+   1. ☑ C is correct. The primary purpose of the UBE gateway is to connect two different VoIP networks, which may use the same signaling protocols or different signaling protocols.
+      ☒ A, B, and D are incorrect. While gateways can be used to connect any other three networks or services, the Cisco UBE gateway does not serve these purposes.

+   2. ☑ A is correct. The Cisco ISR must have the right feature set, which requires a specific version (or higher) of the IOS with that feature set included.
+      ☒ B, C, and D are incorrect. No software or hardware module must be added and the Security Device Manager (SDM) is not required.

+   3. ☑ B, C, and D are correct. You can use H.245, SIP Notify, or KPML to transfer DTMF signals through the UBE gateway.
+      ☒ A is incorrect. SS7 signaling is not directly supported on the UBE gateway as part of the border controller functionality.

+   4. ☑ A and B are correct. Both IP precedence and DSCP marking are supported for QoS on the Cisco UBE.
+      ☒ C and D are incorrect. TCC marking is not a QoS method supported on Cisco routers. Six Sigma is a management and processing methodology and has no bearing on QoS.

# 642-436: Configure Gatekeeper to Support an IP-to-IP Gateway

+   5. ☑ D is correct. The gatekeeper uses v4-zones to know when to route to the UBE and when the VoIP call can be handled internally.
+      ☒ A, B, and C are incorrect. sRTP and cRTP are not required parameters for gatekeeper configuration in relation to the Cisco UBE gateway. IPX interfaces are not used for VoIP networks.

# 642-436: Configure IP-to-IP Gateway to Provide Address Hiding

+   6. ☑ A is correct. The simple address-hiding command is used to hide IP addresses.
+      ☒ B, C, and D are incorrect. Address hiding, hide ip, and hide-ip are invalid commands. They perform no function on Cisco IOS routers or within the Cisco UBE gateway.