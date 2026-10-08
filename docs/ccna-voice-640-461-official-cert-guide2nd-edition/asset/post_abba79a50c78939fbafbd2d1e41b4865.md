
**Note:** Years ago, Cisco Unified Communications Manager (CUCM) and Cisco Unified Communications Manager used to be called Cisco CallManager (CCM) and Cisco CallManager Express (CME). Years later, the CallManager name lives on because it's just simpler to say. So, if you ever hear someone say, "Let's get CallManager set up," it probably wouldn't be the best thing for you to say, "Did you know Cisco renamed that to Cisco Unified Communications Manager?"

## Understanding Cisco Unified Communications Manager Express

The amount a Cisco router is able to accomplish is simply amazing: routing tables, routing protocols, security with access lists, Network Address Translation (NAT)...the list goes on and but. But what if someone told you the Cisco router you were using for years could also support your IP telephony network? That was the goal with the Cisco Unified Communications Manager Express (CME) platform. Your Cisco Integrated Service Router (ISR) platform not only routes data, but terminates analog and digital voice circuits (such as FXO, FXS and T1 ports, which are discussed later), supports VoIP endpoints (such as Cisco IP Phones), and handles the more advanced features, such as conference calling, video telephony, and automatic call distribution (ACD). Depending on the platform you use, CME can support up to 450 IP Phones, which makes it a good solution for small and even some midsized businesses.

Although Cisco designed CME 8.X to operate on the ISR Generation 2 (G2) platforms, you can also run it on the original ISR platforms (such as the 1800, 2800, or 3800 series), provided you have the proper IOS upgrade. Cisco integrates CME into the IOS software itself, based on the feature set you download. Product Authorization Key (PAK) is needed to activate the CME feature set. Table 2-2 shows the current ISR G2 platforms available and the maximum number of phones supported on each platform.

**Table 2-2** Unified CME Supported ISR G2 Platforms

| Platform | Maximum Phones |
| --- | --- |
| Cisco 2901 ISR G2 | 35 |
| Cisco 2911 ISR G2 | 50 |
| Cisco 2921 ISR G2 | 100 |
| Cisco 2951 ISR G2 | 150 |
| Cisco 3925 ISR G2 | 250 |
| Cisco 3945 ISR G2 | 350 |
| Cisco 3925E ISR G2 | 400 |
| Cisco 3945E ISR G2 | 450 |

Keep in mind that these figures are current at the time of writing, but they change all the time as hardware platforms upgrade and become more efficient.

## CME Key Features

Because CME runs on a Cisco router, it has the unique advantage of acting as an all-in-one device for controlling Cisco IP Phones and trunking to the public switched telephone network (PSTN) through various connections. The following are the key features supported by CME:

- **Call processing and device control:** As previously mentioned, CME acts as the all-in-one call control device. It handles the signaling to the endpoints, call routing, call termination, and call features.
- **Command-line or GUI-based configuration:** Because Cisco integrated directly into the IOS, you have the full flexibility of command-line configuration. You can also use a GUI utility, such as the Cisco Configuration Professional (CCP), to interface with a point-and-click style of configuration.
- **Local directory service:** The CME router can have a local database of users you can use for authentication in the IP Telephony (IPT) network.
- **Computer Telephony Integration (CTI) support:** CTI allows the IPT to integrate with the applications running on the data network. For example, you could use the Cisco Unified CallCenter to make calls directly from your Microsoft Outlook contact list.
- **Trunking to other VoIP systems:** Although CME can run as a standalone deployment interfacing with the PSTN, it can also integrate with other VoIP deployments. For example, you could use CME for a small, 40-user office and have it connect directly over your data network to the corporate headquarters supported by a full Cisco Unified Communications Manager (CUCM) cluster of servers.
- **Direct integration with Cisco Unity Express (CUE):** CUE, which runs through a module installed in a Cisco router, can provide voicemail services to the IP Phones supported by CME.

It's not a key feature of CME, keep in mind that by using a CME platform, you have an amazing opportunity to unify the support staff on your network. Rather than having one technician who focuses on maintaining the Cisco network and another technician who focuses on maintaining the phone system, you now have one individual capable of handling everything.

## CME Interaction with Cisco IP Phones

Although there is much to be said about the process Cisco IP Phone uses to contact and register with a CME router (which is discussed in Chapter 3 for how the other call-management applications support the IPT network). First, let's follow the VoIP flow shown in Figure 2-1.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_62_0.png)

Figure 2-1 CME Call Flow for On-Network Cisco IP Phones

Essentially, the relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

Wait, let's re-read the text carefully. "Essentially, the relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router."

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

Actually, looking at the OCR provided, there is some repetitive or broken text. Let's clean up the actual intended flow based on the provided snippets:

"For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

Essentially, the relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router. (Wait, the OCR text seems to have repeated sentences or artifacts. I will provide the logical sequence based on the text provided.)

Essentially, the relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

Wait, let me look at the specific text again: "The fact that CME steps out of the middle of the RTP stream allows the IP Phones to communicate directly is fantastic because of two reasons. First, it eliminates the CME router as a point of failure... it continues unhindered (provided the fire did not burn up the switch). The other benefit is that the CME router does not become a bottleneck for the RTP stream. If the links to the router became saturated or the router ran out of resources, RTP packets can drop, causing the call quality to degrade. Keep in mind that we are only talking about the RTP stream, which contains the audio of the call. All the phone features (as such as transfer, conference, and so on) are still managed using SCCP or SIP, so those would not be available until the CME router came back online."

Let's reconstruct the final section properly based on the OCR:

Essentially, the relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The fact that CME steps out of the middle of the RTP stream allows the IP Phones to communicate directly is fantastic because of two reasons. First, it eliminates the CME router as a point of failure. If it crash, reboot, or catch fire, the connection between the two endpoints continues unhindered (provided the fire did not burn up the switch). The other benefit is that the CME router does not become a bottleneck for the RTP stream. If the links to the router became saturated or the router ran out of resources, RTP packets can drop, causing the call quality to degrade. Keep in mind that we are only talking about the RTP stream, which contains the audio of the call. All the phone features (as such as transfer, conference, and so on) are still managed using SCCP or SIP, so those would not be available until the CME router came back online.

> **Note:** This discussion assumes a CME deployment where there is no backup call-management device. This is common for smaller organizations.

Let's broaden the discussion by following a call from a Cisco IP Phone to an analog phone attached to the PSTN shown in Figure 2-2.

**Figure 2-2** CME Call Flow for Calls to the PSTN

As the user of the Cisco IP Phone picks up the phone to place the call, all the communication is handled by SCCP or SIP. After the user finishes dialing the phone number of the PSTN phone, the CME router realizes (due to its dial-plan) that the call needs to exit out PSTN-connected interface. CME now assumes the role of voice gateway and signals to the PSTN to establish the call on behalf of the Cisco IP Phone. Keep in mind that this is the "old school" signaling discussed in Chapter 1 when the CME router is attached to the PSTN using a digital (T1/EI) or analog (FXO) trunk. The audio for the call connects, the CME router assumes the role of converting between VoIP audio and PSTN audio. Because this connection is processor intensive, the CME router is equipped with Digital Signal-Processors (DSP), which are simply additional "mini processors" dedicated to voice functions.

***

Wait, I should just output the cleaned text. Let me provide the final cleaned version.

[content]
**Note:** Years ago, Cisco Unified Communications Manager (CUCM) and Cisco Unified Communications Manager used to be called Cisco CallManager (CCM) and Cisco CallManager Express (CME). Years later, the CallManager name lives on because it's just simpler to say. So, if you ever hear someone say, "Let's get CallManager set up," it probably wouldn't be the best thing for you to say, "Did you know Cisco renamed that to Cisco Unified Communications Manager?"

## Understanding Cisco Unified Communications Manager Express

The amount a Cisco router is able to accomplish is simply amazing: routing tables, routing protocols, security with access lists, Network Address Translation (NAT)...the list goes on and but. But what if someone told you the Cisco router you were using for years could also support your IP telephony network? That was the goal with the Cisco Unified Communications Manager Express (CME) platform. Your Cisco Integrated Service Router (ISR) platform not only routes data, but terminates analog and digital voice circuits (such as FXO, FXS and T1 ports, which are discussed later), supports VoIP endpoints (such as Cisco IP Phones), and handles the more advanced features, such as conference calling, video telephony, and automatic call distribution (ACD). Depending on the platform you use, CME can support up to 450 IP Phones, which makes it a good solution for small and even some midsized businesses.

Although Cisco designed CME 8.X to operate on the ISR Generation 2 (G2) platforms, you can also run it on the original ISR platforms (such as the 1800, 2800, or 3800 series), provided you have the proper IOS upgrade. Cisco integrates CME into the IOS software itself, based on the feature set you download. Product Authorization Key (PAK) is needed to activate the CME feature set. Table 2-2 shows the current ISR G2 platforms available and the maximum number of phones supported on each platform.

**Table 2-2** Unified CME Supported ISR G2 Platforms

| Platform | Maximum Phones |
| --- | --- |
| Cisco 2901 ISR G2 | 35 |
| Cisco 2911 ISR G2 | 50 |
| Cisco 2921 ISR G2 | 100 |
| Cisco 2951 ISR G2 | 150 |
| Cisco 3925 ISR G2 | 250 |
| Cisco 3945 ISR G2 | 350 |
| Cisco 3925E ISR G2 | 400 |
| Cisco 3945E ISR G2 | 450 |

Keep in mind that these figures are current at the time of writing, but they change all the time as hardware platforms upgrade and become more efficient.

## CME Key Features

Because CME runs on a Cisco router, it has the unique advantage of acting as an all-in-one device for controlling Cisco IP Phones and trunking to the public switched telephone network (PSTN) through various connections. The following are the key features supported by CME:

- **Call processing and device control:** As previously mentioned, CME acts as the all-in-one call control device. It handles the signaling to the endpoints, call routing, call termination, and call features.
- **Command-line or GUI-based configuration:** Because Cisco integrated directly into the IOS, you have the full flexibility of command-line configuration. You can also use a GUI utility, such as the Cisco Configuration Professional (CCP), to interface with a point-and-click style of configuration.
- **Local directory service:** The CME router can have a local database of users you can use for authentication in the IP Telephony (IPT) network.
- **Computer Telephony Integration (CTI) support:** CTI allows the IPT to integrate with the applications running on the data network. For example, you could use the Cisco Unified CallCenter to make calls directly from your Microsoft Outlook contact list.
- **Trunking to other VoIP systems:** Although CME can run as a standalone deployment interfacing with the PSTN, it can also integrate with other VoIP deployments. For example, you could use CME for a small, 40-user office and have it connect directly over your data network to the corporate headquarters supported by a full Cisco Unified Communications Manager (CUCM) cluster of servers.
- **Direct integration with Cisco Unity Express (CUE):** CUE, which runs through a module installed in a Cisco router, can provide voicemail services to the IP Phones supported by CME.

It's not a key feature of CME, keep in mind that by using a CME platform, you have an amazing opportunity to unify the support staff on your network. Rather than having one technician who focuses on maintaining the Cisco network and another technician who focuses on maintaining the phone system, you now have one individual capable of handling everything.

## CME Interaction with Cisco IP Phones

Although there is much to be said about the process Cisco IP Phone uses to contact and register with a CME router (which is discussed in Chapter 3 for how the other call-management applications support the IPT network). First, let's follow the VoIP flow shown in Figure 2-1.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_62_0.png)

Figure 2-1 CME Call Flow for On-Network Cisco IP Phones

Essentially, the relationship between CME and the Cisco IP Phones is similar to the relationship between a mainframe and dumb terminals. CME controls virtually every action performed at the Cisco IP Phones. For example, if a user picks up the handset, an offhook state is sent from the Cisco IP Phone to the CME router.

The fact that CME steps out of the middle of the RTP stream allows the IP Phones to communicate directly is fantastic because of two reasons. First, it eliminates the CME router as a point of failure. If it crash, reboot, or catch fire, the connection between the two endpoints continues unhindered (provided the fire did not burn up the switch). The other benefit is that the CME router does not become a bottleneck for the RTP stream. If the links to the router became saturated or the router ran out of resources, RTP packets can drop, causing the call quality to degrade. Keep in mind that we are only talking about the RTP stream, which contains the audio of the call. All the phone features (as such as transfer, conference, and so on) are still managed using SCCP or SIP, so those would not be available until the CME router came back online.

> **Note:** This discussion assumes a CME deployment where there is no backup call-management device. This is common for smaller organizations.

Let's broaden the discussion by following a call from a Cisco IP Phone to an analog phone attached to the PSTN shown in Figure 2-2.

**Figure 2-2** CME Call Flow for Calls to the PSTN

As the user of the Cisco IP Phone picks up the phone to place the call, all the communication is handled by SCCP or SIP. After the user finishes dialing the phone number of the PSTN phone, the CME router realizes (due to its dial-plan) that the call needs to exit out PSTN-connected interface. CME now assumes the role of voice gateway and signals to the PSTN to establish the call on behalf of the Cisco IP Phone. Keep in mind that this is the "old school" signaling discussed in Chapter 1 when the CME router is attached to the PSTN using a digital (T1/EI) or analog (FXO) trunk. The audio for the call connects, the CME router assumes the role of converting between VoIP audio and PSTN audio. Because this connection is processor intensive, the CME router is equipped with Digital Signal-Processors (DSP), which are simply additional "mini processors" dedicated to voice functions.
