# ## Multipoint Control Units

The MCU provides support for multiuser conferencing when three or more uses are involved in the conference. The MCU manages the resources used in a conference, and it also negotiates for the best codecs within a call setup. In the Cisco world, an MCU will require DSP (digital signal processor) resources in order to combine the audio signals. The MCU receives audio signals from all participants and combines them into a single outgoing audio signal. The result is a conference call.

While the gateway, gatekeeper, and MCU are defined as logically separate components within the H.323 specification, they may be implemented by a single device. For example, a single Cisco ISR can act as the gateway and the gatekeeper for your VoIP network. As VoIP networks grow larger, they are more likely to implement the different H.323 components as separate physical entities.

> > **exam watch**
> >
> > Remember that the four key components of an H.323 network are the terminals, gateways, gatekeepers, and MCUs. Also remember that the gatekeeper is optional, but when it is implemented all terminals must use it for call processing.

# ## CERTIFICATION OBJECTIVE 6.02

# ## 640-460: Describe H.323 Signaling Protocols

Now that you understand the parts that make up the whole of H.323, it's time to explore how H.323 calls are processed. In this section, you will learn about the way in which calls are processed using the H.225.0 protocol and the H.245 protocol. These two protocols form the core of H.323 VoIP networking.

# ### H.323 Call Setup

As a VoIP administrator, it's important that you understand how a call is actually set up and managed with the H.323 protocol suite. The process begins with the H.225 protocol. When you have a VoIP phone connected to a Cisco switch, which is connected to an H.323 gateway (a Cisco IOS router), which is connected to another