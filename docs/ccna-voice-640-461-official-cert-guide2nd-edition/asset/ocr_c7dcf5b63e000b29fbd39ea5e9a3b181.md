# Requirements for Voice, Video, and Data Traffic

The different traffic types that cross your network every day have their own QoS requirements. Some of these requirements might be very loose; the network would essentially need to fail for the application to stop working. Other requirements might be very tight, requiring high-speed connectivity with low delay for the application to work successfully. This section describes general goals for voice, video, and data.

**Tip:** A plethora of QoS software utilities are available that will analyze your network traffic and report the bandwidth and delay each traffic type receives from the network. A popular tool in the Cisco realm is NetQoS (www.netqos.com).

# Network Requirements for Voice and Video

Unlike data traffic, voice traffic is predictable. Whereas data traffic can jump considerably if a large web download or file transfer is started, voice traffic remains a consistent value for each call entering and leaving the network. The actual amount of bandwidth required for voice is heavily dependent on the codec you are using.

In addition to bandwidth requirements, voice traffic has the following additional one-way requirements:

+   - End-to-end delay: 150 ms or less
- Jitter: 30 ms or less
- Packet loss: 1% or less

Video traffic has identical delay requirements as voice, but consumes a lot more bandwidth. In addition, the bandwidth can vary depending on how much movement is in the video (lots of movement increases the bandwidth required for video considerably).

# Network Requirements for Data

It is impossible to give one sweeping guideline for all data applications, because every data application that exists has its own QoS requirement. When designing for the data applications on your network, divide your applications into no more than four or five broad categories. For example:

+   - Mission-critical applications: These applications are critical to your organization and require dedicated bandwidth amounts.

+   - Transactional applications: These applications are typically interactive with users and rapid response times. For example, a technical support employee might use a database application to retrieve caller information based on previous case ID values.

+   - Scavenger applications: These nonproductive applications typically have no business need, but consume excessive amounts of bandwidth. For example, peer-to-peer file-sharing applications, such as Kazaa, BitTorrent, and LimeWire, fall into this category.

![](bbox=[0.06, 0.563, 0.138, 0.623])