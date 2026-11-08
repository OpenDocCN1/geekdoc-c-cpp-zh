# # TWO-MINUTE DRILL

# ## 642-436: Describe SIP

+   - SIP is defined in RFC 3261, which was accepted as a standard in 2002.
+   - SIP borrows from HTTP, SMTP, DNS, and RTP for its implementation and extends the features of these other standards where required.
+   - A SIP call is simply a communication between two or more SIP peers.
+   - The SIP initiator places the call, and the SIP invitee receives the call.
+   - The SIP location service is used to obtain information about a called party's possible locations.
+   - The SIP method is the function that a SIP request is meant to invoke.
+   - A SIP proxy may be used between two SIP peers.
+   - A SIP registrar is a server that accepts REGISTER method requests and stores the registration information in the location service.
+   - A SIP server is a SIP device that receives requests.
+   - A SIP client is a SIP device that sends requests.
+   - The user agent (UA) is the logical entity that acts as a server (UAS) or client (UAC).
+   - The UAS and UAC may operate in the same device.
+   - SIP uses ASCII text-based messages for requests.
+   - SIP uses URIs for addressing.
+   - The Cisco SIP Proxy Server is a Linux-based server and is not integrated into ISRs.

# ## 640-460: Describe SIP Signaling Protocols

+   - SIP uses a four-layer architecture, and the layers are syntax and encoding, transport, transaction, and transaction user.
+   - The syntax and encoding layer defines how SIP messages are structured.
+   - The transport layer defines how messages should be sent and received.
+   - The transaction layer defines how a dialog should transpire.
+   - The transaction user layer defines how the application interacts with the lower layers.