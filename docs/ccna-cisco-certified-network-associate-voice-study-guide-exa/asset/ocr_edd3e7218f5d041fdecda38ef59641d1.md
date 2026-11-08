**TABLE 4-1** Frequencies, Ranges, and Applications

| Frequency Description | Frequency Range | Application |
|---|---|---|
| Human speech | 200–9,000 Hz | Telephony; audio recording; AM and FM radio |
| PSTN channels | 300–3,400 Hz | Telephony; conferencing |
| Human ear (biological microphone) | 20–20,000 Hz | Listening |
| Nyquist theorem | 300–4,000 Hz | Telephony and other audio capture scenarios |

> > **on the Job**
> >
> > You may have noticed the impact of reducing the supported frequency to 4,000 Hz. Have you ever been in a webinar or online virtual class and noticed that the speaker sounds like he or she is on an AM radio station? This is usually because the speaker is dialing into the conference using a land-line (PSTN) phone.

Quantization is the process of matching the samples to a voltage scale. In every second, for voice communications, 8,000 samples must be matched to voltage levels. Most telephony networks use pulse code modulation (PCM), which assigns each sample to an 8-bit value. Therefore, 8,000 samples times 8-bits equals 64,000 bits or 64 kilobits. Since this happens each second, we say that the bandwidth is 64 kbps (kilobits per second). Just remember that quantization is the process used to convert the samples into actual bits of data.

> > **exam watch**
> >
> > Quantization is the process of converting the samples taken from an analog electrical signal into digital data. Most telephony networks use PCM and generate one bit of data for each sample, equaling a data rate of 64 kbps.

Codecs are fully defined later in this chapter; however, for now, just know that they are the factor that defines how the voice signals are quantized and compressed. One of the most common codecs used, G.711, uses the PCM system. Other codecs may use different quantization or encoding techniques. G.711 is covered more in the later sections of this chapter titled “Codecs Defined” and “Codec Complexity.” Another quantization technique is Adaptive Differential PCM (AD-PCM), and it only requires 32, 24, or 16 kbps. The AD algorithm takes advantage of the predictability of human voice patterns and uses less data to represent the same analog electrical signals. AD-PCM will not be as accurate as PCM, but the bandwidth is reduced. In many cases, you may not be able to perceive a quality difference between G.711 and G.726, but more on that concept in the later section of this chapter titled “Selecting the Best Codec.”