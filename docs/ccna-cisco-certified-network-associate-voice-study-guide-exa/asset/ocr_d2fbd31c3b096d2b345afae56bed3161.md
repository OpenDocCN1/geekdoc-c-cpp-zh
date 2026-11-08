# TABLE 17.4 Problems and Definitions

| Problem | Definition |
|---|---|
| Media errors | Bad optic terminations or RF connectors. Poor shielding or damaged cables. |
| Packet or data loss | A measurement of the number of packets lost compared with the total sent. |
| Protocol mismatch | Using an inefficient protocol or improperly labeling packets for Label Switch Routers (LSRs). |
| Jitter | Variableness in the rate of delay. |
| Port settings | Port settings include perimeter firewall ports and client firewall ports. H.323 requires that UDP ports 1718 and 1719 be open. It also requires that TCP ports 1720 and 1503 be open. RTP and RTCP video and audio streams use dynamic ports from 1024 to 65,535 on TCP or UDP. |
| Configuration settings | Improper configuration settings can wreak havoc on a VoIP network. |
| Packet reordering | When routers are congested or traffic is improperly prioritized, VoIP packets may arrive out of sequence more than they normally would. This disorder results in packet resequencing, which can impact voice quality. |
| MTU issues | When a small maximum transfer unit (MTU) size is configured, it can cause fragmentation. This fragmentation can result in extra processing delay. |
| Bandwidth restrictions | VoIP requires consistency in bandwidth availability in order to operate smoothly. Bursty network communications can impact this and lower voice quality. |
| Router misconfigurations | It is not uncommon to see routers running multiple routing protocols (like RIP, OSPF, or IGRP) when only one or two of the protocols are actually needed. These extra routing protocols can degrade network performance. |
| QoS tags being dropped | Not all devices support QoS tags, and as a router extracts the IP packet out of an Ethernet frame, the QoS information can be lost during re-encapsulation. Be sure to select infrastructure devices that support the QoS technology you plan to implement. |
| IP packet loss | Due to UDP’s connectionless nature and the fact that many VoIP protocols rely on it, IP packets can be lost, and this could be due to slow routers and other slow devices on the infrastructure. |
| Backup over the network | Many organizations are now performing data backups across the network. This activity can generate a large amount of network traffic. The backup packets should be tagged as a lower priority than voice and video. You can configure the interleaf ratio so that five or more voice packets are sent for every one of the backup packets. |
| Hardware failure | For any networking technologies to function, all intermediate hardware devices must continue to function. A common problem causing VoIP and other networking communication symptoms is simple hardware failure. |