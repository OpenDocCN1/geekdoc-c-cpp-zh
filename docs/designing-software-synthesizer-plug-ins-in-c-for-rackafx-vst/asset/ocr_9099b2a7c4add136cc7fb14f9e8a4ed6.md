![](bbox=[0.1885, 0.0535, 0.8115, 0.2035])

Figure 7.4: The VA implementation of SVF with three outputs; the signal flow graph is shown at the left.

The bandpass and lowpass outputs are:

```
$y_{lp}(n) = a_1 y_{lp}(n) + b_1 x(n)$
$y_{bp}(n) = a_2 y_{bp}(n) + b_2 x(n)$
```

We can also generate the missing bandstop filter by another shortcut:

```
$y_{bs}(n) = x(n) - 2R_s y_{bp}(n)$
```

# 7.2 Oberheim SEM State Variable Model

Oberheim's Synthesizer Expander Module (SEM) in 1974 featured a modified state variable design. It allowed for three standard outputs for LPF, HPF and BPF, plus a variable BSF that could produce asymmetric resonant bandstop responses in addition to a perfect notch. Not more importantly, it limited a mechanism in the inner feedback path which connects the output of the BP section to the input in a negative feedback loop. In the analog design, the feedback level is controlled with a potentiometer (variable resistor). Therefore, as this feedback signal increases, the overall resonance or Q will decrease. An issue with the SVF design is that when resonance increases, the gain also increases. With the resonance control at a very high setting, this can lead to clipping and distortion, especially at low frequencies. Only a small amount of feedback is applied, and the output of the cascade of sections is greatly amplified. The SEM filter has a switch that turns on when the output of the BP section becomes large enough and bypasses the resonance potentiometer. Figure 7.5(a) shows a simplified circuit version of the SEM. The Operational Amplifier (OTA) and capacitor in each of the boxes implements voltage controlled filtering the tuned integration sections. You can see the similar succession of HPF, BPF and LPF outputs. The BSF output is formed by summing the HPF and LPF outputs. Resistor $R_s$ provides the global negative feedback path from the LPF output back to the input, which is designed using an inverting summer circuit with an input impedance the same as $Rs$. We are particularly interested in the circuit that forms the inner feedback path from the BP output back to the input.

Figure 7.5(b) shows a block diagram with digital integrators replacing the OTA versions. The use of pair diodes D1 and D2, along fed back via an attenuator that is formed by variable R1/R2. When the output at ysim becomes large, the switch of the two diodes turns on and bypasses part of the signal around the feedback control. Resistors R3 and R4 control the mix of the bipolar and straight signals. The threshold is adjusted by the attenuator. This results in a nonlinearity where the diodes do not turn on and off a perfect switch. In addition, each diode is separately engaged for the negative portion (D1) and the positive portion (D2) of the feedback waveform. We can use any number of wave shapes to emulate the diodes and splitter to route portions of the signal around them, a larger problem arises in that the nonlinearity this creates will cause a problem with the design equations of the filter.