

## 数字音频信号处理原理

The first affordable digital audio devices began appearing in the mid-1980s. Digital signal processing (DSP) mathematics had been around since the 1960s and commercial digital recordings first appeared in the early 1970s, but the technology did not become available for widespread distribution until about 15 years later when the advent of the compact disc (CD) ushered in the age of digital audio. Digital sampling refers to the acquisition of data points from a continuous analog signal. The data points are sampled on a regular interval known as the sample period or sample interval. The inverse of the sample period is the sampling frequency. A compact disc uses a sampling frequency of 44,100 Hz, producing 44,100 discrete samples per channel each second, with a sample interval of about 22.7 microseconds (μs). While digital sampling applies to many different systems, this book is focused on only one of those applications: audio.

During the course of this book, you will learn both DSP theory and applications. This is accomplished by experimenting with your own DSP algorithms at the same time as you learn the theory using the included software, RackAFX™. The goal is to understand how the DSP algorithms translate into C++ code. The resulting plug-ins you write can be used to process audio in real time. Because plug-ins are software variations on hardware designs, it’s worth examining how the hardware systems operate, the typical audio coding formats, and the algorithm building blocks you will be using to implement your own software versions.

### 1.1 Acquisition of Samples

The incoming analog audio signal is sampled with an analog-to-digital converter (ADC or A/D). A/Ds must accurately sample and convert an incoming signal, producing a valid digitally coded number that represents the analog voltage within the sampling interval. This means that for CD audio, a converter must produce an output every 22.7 μs. Figure 1.1 shows the block diagram of the input conversion system with LPF, A/D, and encoder.

Violating the Nyquist criteria will create audible errors in the signal in the form of an erroneously encoded signal. Frequencies higher than Nyquist will fold back into the spectrum. This effect is called aliasing because the higher-than-Nyquist frequencies are encoded “in disguise” or as an “alias” of the actual frequency. This is easiest explained with a picture of an aliased signal, shown in Figure 1.2.

The sampling theorem states that a continuous analog signal can be sampled into discrete data points and then reconstructed into the original analog signal without any loss of information—including inter-sample fluctuations—if and only if the input signal has been band-limited so that it contains no frequencies higher than one-half the sample rate, also known as the Nyquist frequency or Nyquist rate. Band-limited means low-pass filtered (LPF). Band-limiting the input signal prior to sampling is also known as adhering to the Nyquist criteria.

![](img/b54974d0a4317ec82d7ae02126d10a6f_21_0.png)

Figure 1.1: The input conversion system ultimately results in numerical coding of the band-limited input signal.

![](img/b54974d0a4317ec82d7ae02126d10a6f_21_1.png)

Figure 1.2: (a) The Nyquist frequency is the highest frequency that can be encoded with two samples per period. (b) Increasing the frequency above Nyquist but keeping the sampling interval the same results in an obvious coding error—the aliased signal is the result.

Once the aliased signal is created, it can never be removed and will remain as a permanent error in the signal. The LPF that band-limits the signal at the input is called the *anti-aliasing filter*. Another form of aliasing occurs in movies. An analog movie camera takes 30 pictures (frames) per second. However, it must often film objects that are rotating at much higher rates than 30 per second, like helicopter blades or car wheels. The result is visually confusing—the helicopter blades or car wheels appear to slow down and stop, then reverse directions and speed up, then slow down and stop, reverse, and so on. This is the visual result of the high-frequency rotation aliasing back into the movie as an erroneous encoding of the actual event.

### 1.2 Reconstruction of the Signal

The digital-to-analog converter (DAC or D/A) first decodes the bit-stream, then takes the sampled data points or impulses and converts them into analog versions of those impulses. The D/A output is then low-pass filtered to produce the final analog output signal, complete with all the inter-sample fluctuations. As with the A/D diagram, the decoder and D/A are both inside the same device (a chip). Figure 1.3 shows the conceptual block diagram of the decoding end of the system.

The output filter is called the reconstruction filter and is responsible for re-creating the seemingly missing information that the original sampling operation did not acquire—all the inter-sample fluctuations. The reason it works is that low-pass filtering converts impulses into smeared out, wiggly versions. The smeared out versions have the shape f(x) = sin(x)/x which is also called the sinc() function and somewhat resembles the profile of a sombrero, as shown in Figure 1.4.

![](img/b54974d0a4317ec82d7ae02126d10a6f_22_0.png)

Figure 1.3: The digital bit-stream is decoded and converted into an analog output using a low-pass filter to reconstruct the analog signal.

![](img/b54974d0a4317ec82d7ae02126d10a6f_22_1.png)

Figure 1.4: The ideal reconstruction filter creates a smeared output with a damped oscillatory shape. The amplitude of the sin(x)/x shape is proportional to the amplitude of the input pulse.

![](img/b54974d0a4317ec82d7ae02126d10a6f_22_2.png)

Figure 1.5: The sin(x)/x outputs of the LPF are summed together to reconstruct the original band-limited input waveform; the inter-sample information has been reconstructed.

When a series of impulses is filtered, the resulting set of sin(x)/x pulses overlap with each other and their responses all add up linearly. The addition of all the smaller curves and damped oscillations reconstructs the inter-sample curves and fluctuations (Figure 1.5).

### 1.3 Signal Processing Systems

Signal processing systems combine data acquisition devices with microprocessors to run mathematical algorithms on the audio data. Those algorithms are the focus of this book. Today's plug-ins are descendents of stand-alone hardware effects processors which are based on DSP chips. A DSP chip is a highly specialized processor designed mainly to run DSP algorithms. A DSP would function poorly as a central processing unit (CPU) for a personal computer because it only has a small but highly specialized instruction set. DSP devices (or just “DSPs”) feature a core processor designed to multiply and accumulate data because this operation is fundamental to DSP algorithms. Because this process is repeated over and over, modern DSPs use pipelining to fetch the next data while simultaneously processing the current data. This technique greatly improves the efficiency of the system. A typical signal processing system consists of the following components (Figure 1.6):
- Data acquisition devices (A/D and D/A)
- A DSP chip
- Memory to store the algorithm program (program memory)
- Memory to store the algorithm data (data memory)
- A user interface (UI) with buttons, knobs, switches, and graphic displays

Music synthesis devices are an embedded version of a CPU+DSP arrangement. The microcontroller or microprocessor manages the UI and keyboard, while the DSP performs the audio synthesis and effects algorithms. Practical implementations now involve multiple DSPs, some of which are custom designed specifically for sound synthesis. An example block diagram is shown in Figure 1.7.

![](img/b54974d0a4317ec82d7ae02126d10a6f_23_0.png)

Figure 1.6: A simple signal processing system. The algorithm in this case is inverting the phase of the signal; the output is upside-down.

![](img/b54974d0a4317ec82d7ae02126d10a6f_23_1.png)

Figure 1.7: Block diagram of a synthesizer.

