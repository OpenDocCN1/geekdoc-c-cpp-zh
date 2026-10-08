at http://www.willpirkle.com/synthbook/ for assistance. Figures 6.31 and 6.32 show the NanoSynth GUI in RackAFX, VS3 and AU after this chapter is complete. In subsequent chapters we continue to fill in the rest of the controls. For RackAFX, several of the controls have been embedded in the LCD control—make sure you understand how to do this from Chapter 2 we will add more and more controls inside the LCD. These will always consist of global synth parameters and not individual component controls.

![](bbox=[0.318, 0.047, 0.953, 0.225])

Figure 6.33 shows the detailed connection diagram of NanoSynth. It shows the controls from Table 6.3 to connect to the underlying synth objects. You can see the addition of the intensity control as well.

You should be getting into the flow of how the projects progress now. For all platforms, the first thing is to implement the GUI controls. Refer back to Chapters 2 and if you need help. Once you have the GUI control code, you are ready to start adding the code for the new modules and connections. You will need to add four new files (or create them manually) for the new objects:

+   - EnvelopeGenerator.h and .cpp
- DCA.h and .cpp

Figure 6.30: The NanoSynth project gets two new additions; EG and DCA modules.

Table 6.3: The new additions of continuous and enumerated string parameters for the NanoSynth GUI.

Figure 6.31: One possible NanoSynth GUI in RackAFX; notice that several controls are embedded in the LCD control.

Figure 6.32: The NanoSynth GUI for the VST3 and AU projects.

# 6.15 NanoSynth: EG/DCA Audio Rendering

For all platforms, the core audio rendering code is the same. Compare with the code in the last chapter (here only new code is bold).

+   - the EG is part of the articulation block, so we need to render it in the output in the same chunk of code
- the EG output is multiplied by the intensity control variable

![](bbox=[0.538, 0.247, 0.953, 0.381])

```
$p = \frac{(bipolarControl+1)}{4}\nL_{out} = \cos(p)\nR_{out} = \sin(p)$
```

```
$attenuation_a = \frac{-x}{20\log_{10}(x^2)}\nx=0, \quad 0 < x \le 127$
```

```
CDCA::CDCA(void) {
    // initialize variables
    m_dAmplitudeControl = 1.0;
    m_dAmpMod_dB = 0.0;
    m_dGain = 1.0;
    m_dAmplitude_dB = 0.0;
    m_dEGMod = 1.0;
    m_dPanControl = 0.0;
    m_dPan = 0.0;
    m_uMIDIVelocity = 127;
}
```