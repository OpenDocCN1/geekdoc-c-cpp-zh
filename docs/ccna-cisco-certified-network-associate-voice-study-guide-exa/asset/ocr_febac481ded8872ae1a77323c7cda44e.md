# 642-436: Choose the Appropriate Codec for a Given Situation

+   11. Which of the following are important considerations when selecting a VoIP codec? (Choose all that apply.)
+   
+       A. Device support
+       B. Network packet loss
+       C. User training
+       D. Network activity

+   12. What formula is used to calculate the number of packets required per second for a given codec?
+   
+       A. `1 / sample_size / samples_in_packet`
+       B. `Packet_Size * Packets_Per_Second`
+       C. `sample_size * samples_in_packet * codec_bit_length / 8 + mgt_overhead`
+       D. `100 / 5 * 6`

+   13. What formula is used to calculate the size of each packet for a given codec?
+   
+       A. `1 / sample_size / samples_in_packet`
+       B. `Packet_Size * Packets_Per_Second`
+       C. `sample_size * samples_in_packet * codec_bit_length / 8 + mgt_overhead`
+       D. `100 / 5 * 6`

# LAB QUESTION

You have chosen the G.729 codec for your Cisco VoIP network. Up to seven calls may be made on the network at any given time. You must calculate three values: the number of packets required per second, the size of each packet, and the total bandwidth consumed with a maximum call load. All default settings are in use for sampling on the Cisco equipment in the environment. What are your answers to these questions assuming that cRTP is not used and Ethernet is the Layer 1 and 2 technology in use?