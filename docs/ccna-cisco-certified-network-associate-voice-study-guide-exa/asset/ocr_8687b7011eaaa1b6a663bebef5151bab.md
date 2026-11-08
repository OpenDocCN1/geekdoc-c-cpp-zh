# FIGURE 6-1

An MGCP call process example

![](bbox=[0.252, 0.135, 0.875, 0.694])

+   4. The CA sends an RQNT message to the gateway, which responds with an ACK message.
+   5. The CA sends a CRCX message to the gateway, which responds with an ACK message. The calling phone goes into receive only mode.
+   6. A CRCX message is sent to the dialed phone, and an ACK message is sent back to the CA. The dialed phone goes into send/receive mode.
+   7. The CA sends an MDCX message to the gateway of the calling phone, which sends back an ACK, and the calling phone stays in receive only mode.