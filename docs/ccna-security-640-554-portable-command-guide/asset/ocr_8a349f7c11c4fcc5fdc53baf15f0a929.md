# ## IKE Negotiation Phases

To establish an IPsec VPN tunnel, IKEv1 and IKEv2 both require two negotiation phases.

| | |
|---|---|
| **IKE Phase 1** | • Goal is to establish an IKE SA.<br>• Phase can be completed in *main mode* or in *aggressive mode*.<br>• Two IPsec peers perform the initial negotiation of SAs.<br>• SA negotiations are bidirectional; data may be sent and received using the same encryption key. |
| **IKE Phase 2** | • Goal is to establish an IPsec SA.<br>• Phase is also called *quick mode*.<br>• SAs are negotiated by the IKE process Internet Security Association and Key Management Protocol (ISAKMP).<br>• In this phase, the SAs that IPsec uses are unidirectional, and therefore a separate key exchange is required for each data flow. |

# ## IKEv1 Phase 1 (Main Mode and Aggressive Mode)

The basic purpose of IKEv1 Phase 1 is to negotiate IKE policy sets, authenticate the peers, and set up a secure channel between the peers.

IKEv1 Phase 1 operates in either main mode or aggressive mode:

| | |
|---|---|
| **Main mode** | • Negotiation exchanges six messages between peers.<br>• These exchanges define what encryption and authentication protocols are acceptable, how long keys should remain active, and whether perfect forward secrecy (PFS) should be enforced. |
| **Aggressive mode** | • Negotiation exchanges three messages between peers.<br>• The initiator passes all data that is required for the SA.<br>• The responder sends the proposal, key material, and ID and authenticates the session in the next packet.<br>• The initiator replies by authenticating the session. |

**NOTE:** Main mode protects the identity of the peers, whereas aggressive mode does not. The use of main mode or aggressive mode is a tradeoff between performance and security.