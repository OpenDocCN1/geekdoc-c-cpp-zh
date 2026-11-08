+   2. The interesting traffic initiates IKE Phase 1 between the peer routers. The IPsec peers negotiate the established IKE security association (SA) policy. Once the peers are authenticated, a secure tunnel is created by using Internet Security Association and Key Management Protocol (ISAKMP).
+   
+   3. The peers then proceed to IKE Phase 2. The IPsec peers use the authenticated and secure tunnel to negotiate IPsec SA transforms. The negotiation of the shared policy determines how the IPsec tunnel is established.
+   
+   4. The IPsec tunnel is created, and data is transferred between the IPsec peers based on the IPsec parameters that are configured in the IPsec transform sets.
+   
+   5. The IPsec tunnel terminates when the IPsec SAs are deleted or when their lifetime expires.

# Planning an IPsec VPN

When planning to deploy a site-to-site IPsec VPN, remember the following:

|  |  |
|---|---|
| **Verify connectivity between peers** | Ensure that IP protocols 50 (ESP) and 51 (AH) and UDP port 500 (ISAKMP) traffic are permitted and not blocked by an access control list (ACL). |
| **Define interesting traffic.** | Define which traffic will trigger a VPN session (interesting traffic) and which traffic will travel outside the tunnel (non-interesting traffic). |
| **Determine the cipher suite requirements.** | Choose a cipher that suits the network security policy of the organization. |
| **Manage monitoring, troubleshooting, and change.** | Consider all three areas in the planning process. |

Interesting traffic is defined by crypto ACLs in site-to-site IPsec VPN configurations.
Crypto ACLs perform these functions:

|  |  |
|---|---|
| **Outbound** | Selects outbound traffic that IPsec should protect. Traffic that is not selected is sent in plaintext. |
| **Inbound** | If you want, you can create inbound ACLs to filter and discard traffic that should have been protected by IPsec. |

**NOTE:** Traffic matching a permit action in the ACL is protected and sent through the VPN. Traffic matching a deny action in the ACL is sent outside the VPN in cleartext.