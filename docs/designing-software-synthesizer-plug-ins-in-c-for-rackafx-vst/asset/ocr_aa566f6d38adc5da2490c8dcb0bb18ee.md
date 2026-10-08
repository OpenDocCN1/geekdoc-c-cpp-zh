The LFO is shown with a pair of triangle waves only because this is a common waveform for modulation, and it distinguishes the LFO from the pitched oscillator visually. Figure 1.4 (b) you can see two other types: OSC A depicts an audio sample loaded from a WAV file, while OSC(noise) is a noise generator. The LFO is placed to the left, the control arm is still upward since it is a controller. It is also implied in this diagram that the controller modulates all the oscillators in the stage above the controller.

# 1.3 Filters

Filters modify the frequency content of an audio signal—thus they are modifiers. There are several basic filter types that we will design in Chapter 7. These include:

+   - lowpass: attenuates high frequencies, may be resonant
- highpass: attenuates low frequencies, may be resonant
- bandpass: allows a band of frequencies to pass through by attenuating both low and high frequencies, may be resonant but usually is not
- bandstop: attenuates a band of frequencies by allowing both low and high frequencies to pass through, may be resonant but usually is not

Although we get into the details in Chapter 7, you can see the lowpass and highpass may be resonant—this produce a resonant peak near the edge of the band of frequencies they are attenuating. The resonant peak may be soft or highly sharply peaked. The bandpass and bandstop filters may technically become resonant, though this is uncommon (we will be introducing one kind of bandstop filter in Chapter 7). Figure 1.5 shows the filters in the book. It depicts a lowpass filter—notice the noise in the curve. Even though it depicts a lowpass, it is implied that it is any kind of filter or a filter that can be changed from one to another. In Figure 1.5(a) you see a single LFO modulating a filtering. The implied modulation is the cutoff frequency of the filter which is special that the filter operates under. We will design both monophonic and stereo synthesizers; in the case we need two filters, one for each channel. In Figure 1.5(b) the LFO modulates both left and right filters once after the implied modulation is cutoff.

# 1.4 Amplifiers

Amplifiers amplify or attenuate a signal so they are also modifiers. Early analog types are called Voltage Controllers or VCAs. We will be implementing Digital Oscillators and DCAs. Our DCA controls the output output of the synth as well as handling panning functions. It can be mono or stereo in but always will be stereo out. A controller can be connected to modulate and control the amplitude and/or panning. Figure 1.6 shows a DCA connected to the filter and DCA. The oscillators feed the filter. One LFO modulates the oscillators, while another modulates the filter and DCA simultaneously. For the DCA, the modulation is implied to be amplitude modulation. We will implement both amplitude and panning modulation in our synths.