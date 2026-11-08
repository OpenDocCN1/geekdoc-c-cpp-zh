# SELF TEST ANSWERS

# 640-460: Identify the Factors that Impact Voice Quality

+   1. ☑ B is correct. Jitter references the variance in delay of arriving packets. For example, if the first packet in a stream arrives, then the second arrives 32 ms later, and then the third arrives 38 ms later, the jitter was 6 ms.
+   
+      ☑ A, C, and D are incorrect. Packet loss refers to dropped packets that do not make it to the destination. RTT is round-trip time and refers to the time it takes to go from point A to point B and back again. Quantization has nothing to do with data delivery on IP networks.
+   2. ☑ C is correct. A jitter buffer attempts to counter the jitter on the network by queuing up a few packets before beginning the audio stream.
+   
+      ☑ A, B, and D are incorrect. 802.1X is a security protocol. 802.1Q is a bridging and VLAN protocol. Delay buffers are not defined in VoIP systems.
+   3. ☑ A is correct. Delay defines the time it takes for a packet to traverse the network, and it is quantified in milliseconds (ms).
+   
+      ☑ B, C, and D are incorrect. Jitter is the variance in delay. Variance is the difference between two values. Packet loss is a reference to dropped packets.
+   4. ☑ A is correct. Quality of service (QoS) can help improve throughput. It does not increase bandwidth, but it uses it more effectively.
+   
+      ☑ B, C, and D are incorrect. Jitter buffers help to counter the impact of jitter. Packet regenerators, such as the PLC algorithm in Cisco systems, can attempt to regenerate missing audio. Digital signal processors (DSPs) are used within Cisco ISRs to encode audio streams.

# 642-436: Describe Voice Quality Considerations

+   5. ☑ D is correct. The PLC can correct 20-50 ms of lost audio; therefore, the upper limit is 50 ms.
+   
+      ☑ A, B, and C are incorrect. Because 50 ms is the upper limit, 20, 10, and 40 are incorrect.
+   6. ☑ A is correct. Less than 10 percent packet loss is usually considered acceptable.
+   
+      ☑ B, C, and D are incorrect. More than 10 percent, which includes less than 20 or 25 percent, would be unacceptable.