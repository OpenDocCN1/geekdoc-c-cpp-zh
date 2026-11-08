network segments converge, such as a single router connecting all segments). In this case, you can use a lower bandwidth codec but, again, the preference is to eradicate the choke point through hardware upgrades or replacements.

+   - **Sample sizes** You must consider the sample size used by the codec. In addition to compression, the sample size impacts the packet size and the number of packets needed to transmit one second of voice data. Networks with higher packet loads may be configured with a codec using more but smaller packets.

It’s important to discuss the last bullet point in more depth. The impact of the packet size on network communications is an important factor to understand when selecting codecs for your VoIP infrastructure.

Multimedia data packets come in varying sizes. We generally speak of a long packet or a short packet, and each packet type has its benefits and drawbacks. Since management information is related to each frame or packet, longer packets incur less overhead. This conclusion is simple math. If you have a total amount of data that you wish to transmit and you transmit that data with short packets, you will incur more overhead. That same amount of data sent with long packets incurs less overhead, since there are fewer packets. To clearly understand this concept, consider the fictional packet sizes in this table:

| Total Data | Packet Size | Management per Packet | Total Packets | Total Management |
|---|---|---|---|---|
| 100 KBps | 10 KBps | 1 KBps | 10 | 10 KBps |
| 100 KBps | 2 KBps | 1 KBps | 50 | 50 KBps |

As the table shows, a packet size of 10 KBps results in 10 KBps of management overhead, assuming a fictional 1k measurement for management data per useful data packet. However, a 2k packet size increases the management overhead by five times (interestingly, the same factor by which it reduced the packet size). The resulting principle is that long packets usually incur less management overhead than short packets.

Long packets also reduce the packet-processing load. The devices that forward the packets on the network must de-encapsulate the packets from the frames and re-encapsulate them to send them on to their destination. The result of using long packets is that there are fewer iterations of the de-encapsulation and re-encapsulation process per total data payload. Think back to the table that listed management overhead for a long packet opposed to a short packet. The same factor applies here. The long packet configuration would demand only 10 iterations of the packet processing, and the short packet would require 50 iterations.