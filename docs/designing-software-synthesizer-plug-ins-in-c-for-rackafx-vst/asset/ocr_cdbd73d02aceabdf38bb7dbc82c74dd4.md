have both inputs and outputs, whereas synthesizer plug-ins are output-only devices. Audio samples can be represented in a variety of formats. In the earliest analog digital converters, the data with the most negative value represented as 00000..0 and the most positive value as 11111..1 which worked well in some control circuits and display outputs. In digital audio samples, we would like to represent both positive and negative values and most importantly the 0.0. Using Pulse Code Modulation (PCM) as a signal can be encoded so that it contains polarities as well as the 0.0 value. Your audio input hardware does this and converts the incoming audio data into PCM-based samples. These samples are integers whose range depends on the bit depth of the analog converter. The ranges for a few different bit-depths are shown in Table 1. You can see that the table is skewed in the negative direction. This is because there are an even number of quantization levels for a given bit depth:

number of quantization = 2^N
N = bit depth

We have assigned one these levels to the value of 0, we have an odd number of levels to split across the range. The reason the negative side gets the extra value has to do with the way PCM is encoded in two's complement fashion. See Designing Audio Plug-Ins in C++ for a detailed discussion.

In order to allow Digital Audio Workstations (DAWs) and their plug-ins to operate on any bit-depth of incoming data, the audio is converted to a floating point or double point number on the range of -1.0 to +1.0, which is accomplished by simply scaling the PCM value by the absolute value of the negative limit. This actually produces a range of values from -1.0 to +0.9999999 for 24 bit audio. We are going to round this to the range of -1.+1 to +1.0. In this book that would be denoted as [-1.+] in this bracket format. This means that the outputs of our synthesizer plug-ins must always lie inside the range of [-1.+] or clipping of the signal will occur which introduces distortion. Usually this is easy to detect. However, as shown in Figure 1.14, the signals inside our synth do not necessarily need to fall on this range.

The audio output data formats that are currently supported:

+   - RackAFX: 32-bit floating point (float)
- VST3: 32-bit floating point (float) and 64-bit double precision (double)
- AU: 32-bit floating point (float)

Table 1.1: The ranges of some different digital audio bit-depths.

| Bit Depth | Negative Limit (-) | Positive Limit (+) |
|---|---||
| 16 | -32,768 | +32,767 |

![](bbox=[0.583, 0.023, 0.976, 0.976])