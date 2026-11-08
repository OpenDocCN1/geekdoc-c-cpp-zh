Another possible benefit of long packets is that you achieve greater network loading. More time is spent sending data as opposed to determining where to send data. This greater loading capability means that the network bandwidth may be more evenly consumed and that the network performance may be more predictable.

The negative aspects of long packets become the positive benefits of short packets. Long packets do create more problems when packets are lost. Since there is so much data in an individual packet, the loss of just one packet can greatly impact the quality of a video or audio stream. Shorter packets are less harmful in such situations. In fact, some scenarios where a packet is lost will hardly be noticeable to the user.

When longer packets are used, latency is increased. Latency is a measure of the difference in time from when a packet is transmitted to when the same packet arrives. Most streaming video and audio technologies, as well as VoIP in general, have upper boundaries that must be imposed on latency variables. One way to reduce latency is to shorten the packet size. Smaller packets move through the network faster because of smaller bits to transmit, and QoS processing can “fit” the smaller packets in more easily.

Finally, short packets have less need for fragmentation. Upper-layer (OSI) data must be chunked or fragmented if it is too large for the lower TCP, UDP, or IP layers. Fragmentation incurs extra processing for both the sender and the receiver and can cause unnecessary delay. A simple method for removing much of the fragmentation is to set your application to send data chunks that result in smaller packets, and therefore, less fragmentation.

Ultimately, a simple formula can be used to help you determine network bandwidth and the best codec to use from a bandwidth perspective. The formula is used to determine the bandwidth is as follows:

```
Bytes_Per_Second = Packet_Size_Bytes(sample_size * samples_in_packet -
codec_bit_length / 8 + mgt_overhead) * Packets_Second(1 / sample_size
/samples_in_packet)
```

You may have noticed that I said it is a simple formula and then delivered quite a long formula. When you break the formula into its components, it is rather simple. Let’s look at each part, starting with the Packet_Size_Bytes formula:

```
Packet_Size_Bytes(sample_size * samples_in_packet * codec_bit_length / 8 +
mgt_overhead)
```

This portion is very simple. We take the sample size (for example, 10 ms or .01 second) and multiply it by the samples in a packet (for example, 2) and multiply