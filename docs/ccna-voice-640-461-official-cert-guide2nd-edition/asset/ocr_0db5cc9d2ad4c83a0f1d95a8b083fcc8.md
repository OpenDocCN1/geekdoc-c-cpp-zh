| Bandwidth 128 (kbps) Burst 3200 (Bytes) |
| (pkts matched/bytes matched) 14231/3903582 |
| (total drops/bytes drops) 1253/391292 |

This output allows you to see the success or failure of the QoS policy applied to the outbound-direction of Serial 3/1. Notice the QoS policy is named VoicePriority. It grants strict priority to the first 128 kbps of voice traffic. Notice the number of packets dropped (1253). This indicates a problem; this is roughly 8 percent of your voice packets. On an actual network, this could call degradation issues of active calls.

The drops are most likely caused by one of two things: a congested WAN link or voice traffic exceeding the provisioned amount. A congested WAN link simply means that there is not enough bandwidth to send the calls in the time required, so the packets are dropped. The latter seems almost identical to the first. That is, if you have too many voice calls, won't congest the WAN and not be able to get all the packets through? Although this may be true, the more likely is the Strict Priority queuing configuration. Strict Priority ensures that the VoIP traffic gets the first and fastest 128 kbps available. However, once the voice traffic tries to exceed this amount, the router begins dropping the traffic (even if there is bandwidth available on the WAN link). This ensures that you know exactly how much voice traffic is going over your WAN connections. The data traffic won't have to fight for the scraps of bandwidth left over.

**Note:** All these troubleshooting guidelines also apply to phones registering with CUCM.