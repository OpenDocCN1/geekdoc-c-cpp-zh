+   - Transaction
+   - Transaction user (TU)

Each layer is described in the following sections.

# ### Syntax and Encoding

The syntax and encoding layer is considered layer one or the lowest layer. The Backus-Naur Form (BNF) grammar is used for SIP encoding. The BNF grammar is also defined in RFC 2234. You will not be required to understand the BNF grammar for your Cisco certifications; however, you can find more information in the BNF RFC and in Section 25 of the SIP RFC. Ultimately, this layer simply defines the format of the messages and commands that can be transmitted within SIP dialogs.

# ### Transport

The second layer is the transport layer. This layer defines how a client sends requests and receives responses as well as how servers receive requests and send responses over a network. The transport layer is described in detail in Section 18 of the SIP RFC. The key fact in relation to the transport layer is the requirement for the implementation of UDP and TCP. While SIP may use other protocols, a standards-compliant implementation must use UDP and TCP.

# ### Transaction

The transaction layer is the third layer in the SIP architecture. This layer is responsible for application-layer retransmissions, matching up responses to requests, and processing application-layer timeouts. All tasks performed by UAs take place in a series of transactions. The transaction layer does not exist in all SIP elements. A SIP element is a component of SIP such as a UA, a proxy, or a registrar. SIP proxies come in two forms: stateless and stateful. A stateful proxy maintains the state or session between the UA and the remote element. A stateless proxy does not maintain this state. Stateless proxies do not include a transaction layer because they simply forward messages and do not maintain state for transaction processing.

# ### Transaction User (TU)

The fourth and final layer is the transaction user (TU) layer. The TU layer is the logical entity that creates transactions for transport using the syntax and encoding specified in the SIP RFC. All SIP entities or elements, with the exception of the stateless proxy, qualify as a TU.

# ### SIP Headers

If you've ever performed HTTP debugging or analysis, then you'll be well prepared for understanding the SIP headers. SIP headers are very similar to HTTP headers in that they are constructed as ASCII text and not as binary numbers. With SIP,