# Wireless

Wireless networks are vulnerable to penetration through Internet facing connections just like wired networks; however, wireless networks also introduce entirely new vulnerabilities. Instead of focusing on ports, you must focus on connections. Wireless networks allow client devices to connect to the network without the use of preassigned ports. For this reason, disabling ports is not an option. MAC filtering has been used in the past in an attempt to accomplish security at the same level as port management; however, MAC filtering is very weak since an attacker may monitor the network and discover valid MAC addresses. Once the valid addresses are known, the attacker must reconfigure her device to use an allowed MAC address. For this reason, you should consider MAC filtering as a security myth and not as a security solution.

In fact, many threats are associated with wireless security. I’ll cover just a few of them here:

+   - MAC Filtering
+   - SSID Hiding
+   - All Modern Equipment Uses “Better WEP”
+   - Wireless Networks Can’t Be Secured

# MAC Filtering

Vendors of wireless devices and books on wireless networking often provide a list of the “Top 5” or “Top 10” things you should do to secure your wireless LAN. This list usually includes MAC filtering and SSID hiding or cloaking. The reality is that neither of these provides a high level of security. MAC addresses can easily be spoofed, and valid MAC addresses can be identified in just a few moments. For example, an attacker can eliminate the AP in an infrastructure BSS (Basic Service Set) by looking for the MAC address that sends out beacon frames. This will always be the AP in the BSS. With this filtered out of the attacker’s protocol analyzer, he has only to find other MAC addresses that are transmitting with a destination MAC address equal to that of the AP. Assuming the captured frames are data frames, the attacker now knows a valid MAC address.

MAC filtering will make it more difficult for an attacker to access your network. The attacker will have to go through the process I’ve just outlined (or a similar process) to obtain a valid MAC address to spoof. However, you are adding to your workload by implementing such MAC filtering, and you have to ask, “Am I getting a good return on investment for my time?” The answer is usually no. Assuming you are using TKIP (Temporal Key Integrity Protocol) or CCMP (counter mode with cipher block chaining-message authentication code) with a strong EAP type for authentication (or even pre-shared keys), this will be so much more secure than