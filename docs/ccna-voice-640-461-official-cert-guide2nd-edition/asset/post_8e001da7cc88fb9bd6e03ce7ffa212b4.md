
going to happen, whereas using the loop start method of signaling just connects the wires to receive an incoming call or place an outgoing call.

**Tip**: Many other types of signaling exist in the analog world. These include supervisory signaling (on hook, hook off, ringing), informational signaling (dial tone, busy, ringback, and so on), and address signaling (dual-tone multifrequency (DTMF) and Pulse). These are discussed as part of the CVOICE certification series (for more information, see www.ciscopress.com/bookstore/product.asp?isbn=1587055546).

## The Evolution: Digital Connections

Analog signaling was a massive improvement over tin cans and string, but still plenty plenty problems of their own. First, an analog electrical signal experiences degradation (signal fading) over long distances. To increase the distance the analog signal could travel, the phone company had to install repeaters (shown in Figure 1-5) to regenerate the signal as it became weak.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_38_0.png)

**Figure 1-5** Analog Signal Repeaters

Unfortunately, as the analog signal was regenerated, the repeater device was unable to differentiate between the voice traveling over the wire and line noise. Each time the repeater regenerated the voice, it also amplified the line noise. Thus, the more times a phone company regenerated a signal, the more distorted and difficult to understand the signal.

The second difficulty encountered with analog connections was the sheer number of wires the phone company had to run to support a large geographical area or a business with a large number of phones. Because each phone required two wires, the bundles of wire became massive and difficult to maintain (imagine the hassle of a single pair of wires in the bundle breaking). A solution to send multiple calls over a single wire was needed. Digital connection is that solution.

## Moving from Analog to Digital

Simply put, digital signals use numbers to represent levels of voice instead of a combination of electrical signals. When someone talks about "digitizing voice," they are speaking of the process of changing analog voice signals into a series of numbers (shown in Figure 1-6) that you can use to put the voice back at the other end of the line.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_39_0.png)

# Figure 1-6 Converting Analog to Digital Signals

Essentially, each number sent represents a sound that someone easily made while speaking into a telephone handset. Today's network devices can easily transmit a numeric value any distance a cable can run without any degradation or line noise, which solves the digital degradation issues faced by analog phone connections. Could digital signaling resolve the huge number of wires required by multiple analog connections? Indeed, it can.

Digital voice uses a technology known as time-division multiplexing (TDM). TDM voice networks to carry multiple conversations at the same time over a single, four-wire path. Because the multiple conversations have been digitized, the numeric values are transmitted in specific time slots (thus, the “time division”) that differentiate the separate conversations. Figure 1-7 illustrates three separate voice conversations sent over a digital connection.

> Key Topic

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_39_1.png)

# Figure 1-7 Time-Division Multiplexing Voice Channels

Each of the voice conversations in Figure 1-7 has been digitized and assigned a numeric value and transmitted over the digital PSTN connection. Based on the time the voice data was sent, the PSTN carrier is able to distinguish and reassemble the voice conversations.

**Note:** Although the values in each time slot are shown in decimal in Figure 1-10, they are actually transmitted and interpreted in binary.

Corporations use digital voice connections to the PSTN as T1 circuits in the United States, Canada, and Japan. A T1 circuit is built from 24 separate 64-kbps channels known as a digital signal 0 (DS0). Each of these channels is able to support a single voice call. Corporations in areas outside the United States, Canada, and Japan use E1 circuits, which allow you to use up to 30 DS0s for voice calls.

Although digital technology solves the problems of signal degradation and the inability to send multiple calls over a single line that out analog technology, it creates a new issue: With analog circuits, supervisory signals were passed by connecting the tip and ring wires together. The phone company generated information and address signals through specific frequencies of electricity. By solving the problems associated with analog signaling, digital signaling also removed the typical degrading signaling capabilities. To solve this, two primary styles of signaling were created for digital circuits:

- **Channel associated signaling (CAS):** Signaling information is transmitted with the same bandwidth as the voice.
- **Common channel signaling (CCS):** Signaling information is transmitted using a separate, dedicated signaling channel.

The following sections discuss these two styles of signaling.

## Channel Associated Signaling

T1 digital connections actually "steal" binary bits that would typically have been used to communicate voice information and use them for signaling. Initially, this may seem crazy; if you take the binary bits that are used to resynthesize the voice, won't the voice quality drop significantly? Although the voice quality does drop some, the number of binary bits stolen for signaling information is small enough that the change in voice quality is not noticeable.

**Note:** Because T1 CAS steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS).

The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information, it is often called **robbed bit signaling** (RBS). The voice device running the T1 steals from the voice channel to transfer signaling information.

Actually, the sixth frame (marked with S in Figure 1-10), the eighth bit (also called pulse code) is stolen for the device. This process occurs every sixth frame. For example, the stolen bit relays the signaling. This relays the signaling information for each respective DS0 channel.

![](img/e4ad7862dc47b4e5de0cde3b4550ad65_40_0.png)

| Frame 1 | Frame 2 | Frame 3 | Frame 4 | Frame 5 | Frame 6 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | | S |
| | | | | | S |
| | | | | | S |
| | | | | | S |
| | | | | | S |
| | | | | | S |

Figure 1-8 CAS T1 Signaling Bits

## Common Channel Signaling

CCS dedicates one of the DSO channels from a T1 or E1 link for signaling information. This is often called out-of-band signaling because the signaling traffic is completely separate from the voice traffic. As a result, a T1 connection using CCS has only 23 usable DSOs for voice. Because CCS dedicates a full channel of the circuit for signaling, the "stolen bit" method of signaling using ABCD bits is no longer necessary. Rather, a full signaling protocol sends the necessary information for all voice channels. The most popular signaling protocol is Q.931, which is the signaling protocol used for ISDN circuits.

CCS is the most popular connection between voice systems worldwide because it offers more flexibility with signaling messages, more bandwidth for the voice bearer channels, and higher security (because the signaling is not embedded in the voice channel). CCS also allows PBX vendors to communicate proprietary messages (and features) between their PBX systems using ISDN signaling, whereas CAS does not offer any of these capabilities.

> Tip: When using CCS configurations with T1 lines, the 24th time slot is always the signaling channel. When using CCS configurations with E1 lines, the 17th time slot is always the signaling channel.

Note: Although ISDN is the most popular protocol used with CCS configurations, for example, telephone companies use the Signaling System 7 (SS7) protocol (described later) with CCS configurations to communicate between COs.
