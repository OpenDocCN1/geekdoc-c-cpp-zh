| Parameters: | output for a given input, x(n) |
|---|---|
| • float flnput | Input: the current input sample x(n) |

# # 12.5 Envelope Detection

Software envelope detectors are based on the analog circuits that preceded them. The two basic types of detectors are half-wave and full-wave, depending on whether they track either the positive or negative portion of the input waveform (half-wave) or both portions (fullwave). Many of the classic hardware devices used the half-wave version. Either the positive or negative portion may be tracked. The circuit consists of a diode to half-wave-rectify the signal, followed by a “tank” capacitor. The capacitor charges and discharges along with the audio signal. The attack knob is a potentiometer in series with the diode; it controls the rate at which the cap charges. The release knob is a potentiometer connected to ground through which the cap discharges. The RC combinations (one for the charging side and the other for the discharging side) create the attack and release times of the detector (Figure 12.9). The positive portion of the waveform is detected and tracks the input according to the attack and release times (Figures 12.10 and 12.11).

![](bbox=[0.3, 0.38, 0.7, 0.48])

Figure 12.9: A simple positive half-wave detector.

![](bbox=[0.2, 0.55, 0.8, 0.72])

Figure 12.10: Detector output (solid dark line) with short attack and release times.

![](bbox=[0.2, 0.79, 0.8, 0.98])