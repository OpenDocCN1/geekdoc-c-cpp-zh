The preceding commands would set the complexity to high for voice-card number one. To set the complexity to one of the other three options, simply change the keyword high to medium, flex, or secure. You can view the current codec settings with the show voice dsp command within enable mode.

Voice companding refers to the process of compressing the audio on the transmitting end and expanding the audio on the receiving end. “Compressing” and “expanding” equals “companding.” I know, it sounds like something my 6-year-old would create, but it’s an important part of IP telephony.

G.711 defines two different companding algorithms. Each is based on mathematical formulas or laws, and each is named for this law. The first is μ-law (pronounced mew-law), and the second is a-law. Here, μ-law is a mathematical algorithm used for pulse code modulation (PCM). The algorithm represents analog amplitude values as compact digital codes. Three binary bits represent one of eight different ranges of amplitude values. Four more bits are used to represent an amplitude value within the range specified by the first three bits. The μ-law algorithm is used in T1 lines in the United States and J1 lines in Japan.

A-law is also a mathematical algorithm. The specifications are the same as for μ-law in that the first three bits represent the range, and the last four bits represent an amplitude in that range. A-law companding is used primarily on E1 lines in Europe.

> **exam watch**
> 
> When configuring the G.711 codec, you should know that it uses two different encoding methods known as μ-law and a-law. μ-law is used in the United States and Japan, and a-law is used everywhere else. They simply encode differently—in fact, they encode in an exact opposite way.

# ## CERTIFICATION OBJECTIVE 4.03

# # 640-460: Describe the Function of and Differences between Codecs

In this section, you’ll explore the similarities and differences among the many codecs. You’ll explore the benefits of the features mentioned in the preceding section so that you can best select the appropriate codec as covered in the later section of this chapter titled “Selecting the Best Codec.”