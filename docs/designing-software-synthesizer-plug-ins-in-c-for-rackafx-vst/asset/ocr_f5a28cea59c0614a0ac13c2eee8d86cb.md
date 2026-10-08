# Chapter 9

MiniSynth is based on the architectures of K Volca Keys and Moog MiniMoog synths, MiniSynth features the same MIDI implementation as NanoSynth and uses a modulation matrix to simplify programming and increase flexibility. You can spin off many variations of MiniSynth for your projects. In this chapter, we will replace the NanoSynth voice structure with a new voice object called MiniSynthVoice. This object is derived from the base class CVoice. The CVoice object is de handling much of the core functionality that the rest of the synths use, and each new synth in this chapter will introduce a new derived voice class based on the specific needs of each design. CVoice does so much of the work that creating new voice architectures and synth designs is greatly simplified.

This is a turning point in the book. The underlying synth object code is now set and will not change. You have seen an example of wiring the components in code using intermediate variables and function calls to implement modulation. You have also seen the implementation with the modulation matrix. In the following chapters, we derive new voice objects from the CVoice base class; there is one new voice object per synth. The synths all use the modulation matrix for connections. Polyphony is implemented in a more advanced way than NanoSynth.

However, this is a point where you may easily deviate from the book code and design your own voice objects. You might decide not to use the modulation matrix or to implement polyphony differently. Go for it! This also makes an excellent assignment. The synth voice, modulation matrix connections and GUI parameter list follow the same pattern, so you are free to implement the code as you wish. You might decide to use the book code first, go back and refine it in a way that fits your programming style.

Figure 9.1 shows the simplified block diagram for MiniSynth. You can see that this is very similar to NanoSynth additions include more oscillators and voice modes (oscillator combinations), a sub-oscillator and noise generator. The LFO can also panning in the DCA. Before we look at the complete block diagram, let's look at the CVoice object.

# 9.1 Voice Architectures and CVoice

The MiniSynth voice architecture consists of:

+   - four oscillators
- one filter
- one DCA
- one LFO
- one EG

You can see that it is nearly the same as NanoSynth, but with a few more modulation routings and oscillators. The CVoice object is designed to encapsulate the functionality of a generic synth voice. But what is a generic voice? Let's look at a few commercial synthesizers and study their voice architectures. Figures 9.2–9.6 show the simplified voice architectures for the Korg Polis, Korg MS-20, Yamaha EX-5, Sequential Circuits Prophet VS, and Korg Triton/Karma.

You may see many similarities and differences in the voice architectures, but they are all a combination of oscillators, filters, EGs and DCs. The Korg H.I. architecture might win the prize for most number of sub-components. The CVoice Object consists of the following sub-components shown in Figure 9.7.

+   - four oscillators