
## Encapsulating IPsec Packets

There are two main IPsec framework protocols:

| Protocol | Description |
|---|---|
| **Authentication Header (AH)** | • AH provides data authentication and integrity.<br>• However, it does not provide confidentiality.<br>• AH provides integrity and authentication of the payload using either HMAC-MD5 or HMAC-SHA-1.<br>• AH is IP protocol 51. |
| **Encapsulating Security Payload (ESP)** | • ESP provides confidentiality by encrypting the payload using DES, 3DES, or AES.<br>• ESP can also provide integrity and authentication of the payload using either HMAC-MD5 or HMAC-SHA-1.<br>• ESP can also enforce anti-replay protection by requiring that a receiving host set the replay bit in the header to indicate that the packet has been seen.<br>• ESP is IP protocol number 50. |

**NOTE:** This chapter focuses on ESP, along with other important IPsec protocols.

## Transport Versus Tunnel Mode

ESP and AH can be used in two different modes:

| Mode | Description |
|---|---|
| **Transport mode** | • Security is provided only for the transport layer and above.<br>• Transport mode protects the payload of the packet but leaves the original IP address in the clear.<br>• ESP transport mode is used between hosts. |
| **Tunnel mode** | • Tunnel mode provides security for the complete IP packet.<br>• The original packet is encrypted and then encapsulated in another IP packet.<br>• ESP tunnel mode is used between a host and a security gateway or between two security gateways. |

**NOTE:** The focus in this book is on tunnel mode.

| Algorithm | Description |
|---|---|
| **HMAC-Secure Hash Algorithm 2 (HMAC-SHA-2)** | ▪ SHA-2 HMAC algorithms are the strongest algorithms.<br>▪ The SHA-2 family is based on SHA-1 and adds the SHA-256 bit hash algorithm and SHA-384 bit hash algorithm. |

## Peer Authentication Methods

| Method | Description |
|---|---|
| **Pre-shared keys (PSK)** | ▪ Peers authenticate each other by comparing preconfigured secret keys.<br>▪ The PSK is combined with other information to create the authentication key. |
| **RSA signatures** | ▪ Peers authenticate each other using digital certificates.<br>▪ The sending peer creates an encrypted hash using their private key, attaches it to a message, and forwards it.<br>▪ The remote peer decrypts the hash using the public key and compares it with a recomputed hash. |
| **RSA encrypted nonces** | ▪ Peers authenticate each other using RSA-generated random numbers (called nonces).<br>▪ Public keys must be manually copied to each peer as part of the configuration process.<br>▪ This method is the least popular. |
| **Elliptic Curve Digital Signature Algorithm (ECDSA)** | ▪ ECDSA is the method used for the Digital Signature Standard (DSS).<br>▪ ECDSA improves the communication efficiency:<br>&nbsp;&nbsp;▪ It is quicker than similar-strength RSA operations.<br>&nbsp;&nbsp;▪ It is smaller than RSA signatures. |

## Key Exchange Algorithms

Encryption algorithms require a symmetric shared-secret key to perform encryption and decryption. These algorithms are used within IKE to establish session keys. The following public key exchange methods are available in Cisco IOS Software:

## IKE Negotiation Phases

To establish an IPsec VPN tunnel, IKEv1 and IKEv2 both require two negotiation phases.

| | |
|---|---|
| **IKE Phase 1** | • Goal is to establish an IKE SA.<br>• Phase can be completed in *main mode* or in *aggressive mode*.<br>• Two IPsec peers perform the initial negotiation of SAs.<br>• SA negotiations are bidirectional; data may be sent and received using the same encryption key. |
| **IKE Phase 2** | • Goal is to establish an IPsec SA.<br>• Phase is also called *quick mode*.<br>• SAs are negotiated by the IKE process Internet Security Association and Key Management Protocol (ISAKMP).<br>• In this phase, the SAs that IPsec uses are unidirectional, and therefore a separate key exchange is required for each data flow. |

### IKEv1 Phase 1 (Main Mode and Aggressive Mode)

The basic purpose of IKEv1 Phase 1 is to negotiate IKE policy sets, authenticate the peers, and set up a secure channel between the peers.

IKEv1 Phase 1 operates in either main mode or aggressive mode:

| | |
|---|---|
| **Main mode** | • Negotiation exchanges six messages between peers.<br>• These exchanges define what encryption and authentication protocols are acceptable, how long keys should remain active, and whether perfect forward secrecy (PFS) should be enforced. |
| **Aggressive mode** | • Negotiation exchanges three messages between peers.<br>• The initiator passes all data that is required for the SA.<br>• The responder sends the proposal, key material, and ID and authenticates the session in the next packet.<br>• The initiator replies by authenticating the session. |

**NOTE:** Main mode protects the identity of the peers, whereas aggressive mode does not. The use of main mode or aggressive mode is a tradeoff between performance and security.

This chapter covers the following topics:

## Site-to-Site IPsec VPNs

- IPsec VPN Negotiation Steps
- Planning an IPsec VPN
- Cipher Suite Options

## Configuring IOS Site-to-Site VPNs

- Verifying the VPN Tunnel
- Configuring a Site-to-Site IPsec VPN Using IOS Example
- Configuring a Site-to-Site IPsec VPN Using CCP Example
- Generating a Mirror Configuration Using CCP
- Testing and Monitoring IPsec VPNs
- Monitoring Established IPsec VPN Connections Using CCP

## Site-to-Site IPsec VPNs

Organizations of all kinds often deploy site-to-site virtual private networks (VPNs) when implementing a corporate network across public and private networks. Internet-based VPN environments and Multiprotocol Label Switching (MPLS) VPN environments benefit from the flexibility of deployment and standards-based implementation of cryptographic mechanisms.

The choice of device terminating VPNs becomes a key factor in implementing site-to-site VPNs. Organizations benefit from leveraging their existing network elements and using an integrated approach to VPN deployments. This lesson highlights the use of Cisco IOS routers as site-to-site VPN termination points in IP Security (IPsec) environments.

### IPsec VPN Negotiation Steps

IPsec VPN negotiation can be broken down into five steps, including Phase 1 and Phase 2 of Internet Key Exchange (IKE):

- 1. An IPsec tunnel is initiated when a host sends "interesting" traffic to a destination host. Traffic is considered interesting when it travels between the IPsec peers and meets the criteria that are defined in the crypto ACL.
- 2. The interesting traffic initiates IKE Phase 1 between the peer routers. The IPsec peers negotiate the established IKE security association (SA) policy. Once the peers are authenticated, a secure tunnel is created by using Internet Security Association and Key Management Protocol (ISAKMP).
- 3. The peers then proceed to IKE Phase 2. The IPsec peers use the authenticated and secure tunnel to negotiate IPsec SA transforms. The negotiation of the shared policy determines how the IPsec tunnel is established.
- 4. The IPsec tunnel is created, and data is transferred between the IPsec peers based on the IPsec parameters that are configured in the IPsec transform sets.
- 5. The IPsec tunnel terminates when the IPsec SAs are deleted or when their lifetime expires.

### Planning an IPsec VPN

When planning to deploy a site-to-site IPsec VPN, remember the following:

| | |
|---|---|
| **Verify connectivity between peers** | Ensure that IP protocols 50 (ESP) and 51 (AH) and UDP port 500 (ISAKMP) traffic are permitted and not blocked by an access control list (ACL). |
| **Define interesting traffic.** | Define which traffic will trigger a VPN session (interesting traffic) and which traffic will travel outside the tunnel (non-interesting traffic). |
| **Determine the cipher suite requirements.** | Choose a cipher that suits the network security policy of the organization. |
| **Manage monitoring, troubleshooting, and change.** | Consider all three areas in the planning process. |

Interesting traffic is defined by crypto ACLs in site-to-site IPsec VPN configurations.
Crypto ACLs perform these functions:

| | |
|---|---|
| **Outbound** | Selects outbound traffic that IPsec should protect. Traffic that is not selected is sent in plaintext. |
| **Inbound** | If you want, you can create inbound ACLs to filter and discard traffic that should have been protected by IPsec. |

**NOTE:** Traffic matching a permit action in the ACL is protected and sent through the VPN. Traffic matching a deny action in the ACL is sent outside the VPN in cleartext.
