LCD control—make you understand how to do this from Chapter 2. For VST3 and AU users, you can use the mini knob control for key-enabling and intensity.
Chapter 2 for details and you use the sample code as a guide.

Figure 7.53: The NanoSynth project gets a filter upgrade, with EG modulation routulations.

Figure 7.54: One possible NanoSynth GUI in RackAFX; notice that several controls are embedded in the LCD control.

Figure 7.55: The NanoSynth GUI for the VST3 and AU projects.

Table 7.3: The new additions of continuity and enumerated string parameters for the NanoSynth GUI.

Figure 7.56: The NanoSynth detailed connection graph reveals the new controls from Table 6.x.

Figure 7.56 shows the detailed connection diagram for NanoSynth. It shows how the controls from Table 7.3 connect to the underlying physics. Notice how the EG and LFO outputs are summed before application to the oscillator pitch modulation. You will need to remember this when we approach the Modulation Matrix in Chapter 8.

# CMoogLadderFilter::CMoogLadderFilter(void)

For all platforms, you first implement the GUI controls. Refer back to Chapters 2 and if you need help. Once you have the GUI code in place, you are ready to start adding the code for the new modules and connections. You will also need to add all of the new filter filters (or create them manually) for the new objects.

```
-- init
m_dK = 0.0;
m_dAlpha_0 = 1.0;
```

```
-- Oberheim variables
m_dA = 0.0; m_dB = 0.0; m_dC = 0.0;
m_dD = 0.0; m_dE = 0.0;
```

```
-- set all as LPF types
m_LPF1.m_uFilterType = LPF1; m_LPF2.m_uFilterType = LPF1;
m_LPF3.m_uFilterType = LPF1; m_LPF4.m_uFilterType = LPF1;
```

+   * CVAOnePoleFilter.h and .cpp
* CSEMFilter.h and .cpp
* CKThreeFiveFilter.h and .cpp
* CMoogLadderFilter.h and .cpp