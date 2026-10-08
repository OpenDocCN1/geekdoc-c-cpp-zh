![](bbox=[0.192, 0.038, 0.807, 0.375])

Figure 1.3: A generic synth patch consisting of two sources, a modifier, and three controllers.

# 1.2 Oscillators

Oscillators render audio without an input. We are going to design and use several types of oscillators that synthesize waveforms in various ways:

+   - mathematically
- using lookup tables called wavetable
- by extracting audio samples contained in WAV files
- Frequency Modulation (FM) and Phase Modulation (PM)

Oscillators can be used as both sources and controllers. We are going to divide oscillators into two groups: pitched oscillators and Low-Frequency Oscillators (LFOs). In most cases we will call pitched oscillators simply oscillators. In this book, each synth will have two block diagrams—a simple block diagram and a detailed connection graph. The simple block diagram is easy to read and shows the architecture but does not show every connection, while the detailed connection graph shows all connections and Graphical User Interface (GUI) controls. We will discuss these connection graphs as the chapters progress. Oscillators and LFOs will be shown with the two symbols in Figure [1.4] for the simple block diagrams. In Figure [1.4 (a)] an LFO modulates a single oscillator. The exact type of modulation is not indicated, but in our synth block, this oscillator is an implied connection to modulate the oscillator’s pitch (frequency). This oscillator is shown with a pair of ramp or sawtooth waves in the circle. For our synths, this means one of the mathematically or wavetable generated waveforms. The FM synth called DXSynth will use sinusoidal oscillators, so in that special case, you will see sinusoids instead of ramps.