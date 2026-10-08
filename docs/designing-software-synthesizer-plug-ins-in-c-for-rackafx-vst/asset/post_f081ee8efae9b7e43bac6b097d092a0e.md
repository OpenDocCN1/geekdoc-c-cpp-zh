
and not a DCA. This simple patch is made of two of these building blocks. Chowing named these FM structures, or operators, and they are for the architecture of the DX synths, as the DXSynth in this chapter. The fundamental quality of an FM patch (searing, mellow, muted, sharp, bell, etc.) is a result of the arrangement of multiple operators. Chowing drew signal flows from top to bottom, as the oscillator points downwards. Figure 12.10 shows the Chowing abbreviation. Note that details about the EG and oscillator control frequencies are omitted. Each operator always includes an accompanying EG, the carrier oscillators are always set to the MIDI note pitch, and the modulator oscillators always use ratio of MIDI note pitch; each modulator can be tuned to a different ratio.

Figure 12.9: Block diagram of a simple FM patch with one carrier and one modulator.

Figure 12.10: (a) A simple operator patch (b) Chowing's version.

Figure 12.11: (a) A four operator FM patch with details and (b) the Chowing abbreviation.

In addition to stacking multiple modulators upon modulators, an FM operator can also self-modulate, as in the stacked set of four operators in Figure 12.11. The last operator in the chain (number 4) is self-modulating.

The DX7 features six FM operators arranged in 32 different combinations. The DX100 has FM operators arranged in eight different combinations. Chowing called the combinations algorithms, and the DX synthesizers were branded “Digital Programmable Algorithm Synthesizers”—in fact, “FM” appears nowhere on the synth enclosures. Operators can be placed in series or parallel, and there can be more than one carrier. Figure 12.12 shows two more of these algorithms and the implied that are involved. The DXSynth in this chapter is a close replica of the DX100 using four operators in the same algorithm combinations. These algorithms are shown in Figure 12.13.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_814_0.png)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_814_1.png)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_814_2.png)

## 12.5 DXSynth Specifications

Since DXSynth is based on the DX100, its voice will need four oscillators and four envelope generators. There are no filters. It is a DCA, but it is used for panning and volume control; there is no EG connected to the DCA. Instead, the envelope of the carriers dictate the final time domain envelope. As in the DX100, there is one LFO, which may be used to modulate pitch vibrato or output amplitude (Amplitude Modulation or AM) independently for each operator. Figure 12.14 shows the simplified block diagram, while Figure 12.15 shows the detailed connection. Don't let the simplicity of this synth fool you—it can synthesize much wider variety of sounds than the other synths in the little CPU overhead.

Figure 12.12: (a) four operator patch with multiple modulator outputs summed in parallel (b) four carriers in parallel; the outputs are summed to form the final output.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_815_0.png)

Figure 12.13: The eight algorithms in the DX100 and DXSynth.

Table 12.4 shows the modulation matrix for DXSynth consisting of eight rows. These route the LFO to output destinations (AM or vibrato) on each operator.

Table 12.5 shows the GUI controls. These are mostly repeated sets of operator controls. Figures 12.16 and 12.17 show the GUI designs for RackKFX and VST3/AU respectively. VST3 get a bonus—graphic of the eight DX algorithms is included.

Figure 12.14: DXSynth simplified block diagram.

Table 12.4: The modulation matrix for DXSynth contents disconnected routings for the LFO to feed destinations on each operator.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_815_1.png)

Figure 12.15: DXSynth detailed connection. Notice that the four operator controls labeled Op1 Out, Op2 Out, Op3 Out and Op4 Out ranges from 0 to 9 with a default of 7. This is a special kind of output calculation unique to this project. The DX series of synths have output controls with a 0 to 9 range. In all the previous synths, we used EG1 as the output by default. In DXSynth, these controls produce nearly logarithmic volume changes across that range. Using empirical data collected from the DX100, the function calculateAmplitude() in synth.h replicates the behavior and calculates an amplitude scalar with an input from 0 to 9. This will let you compare your versions of DX algorithms with the real product. Another issue that DXSynth involves the output EGs. You can see from looking at the algorithm diagram that in some cases, there is more than one carrier. The carrier EGs are actually output EGs that control the time envelope for each carrier. This lets you create interesting patches because you are in control of the separate sets of harmonics which might fade away faster during the release portion.

![](img/b42d0dca53f4a889d8162d55f7c8c05d_816_0.png)

| Source | Destination/Intensity | Transform/Range | enabled |
| :--- | :--- | :--- | :--- |
| SOURCE_LFO | DEST_C1_OUTPUT_AMP | TRANSFORM_BIPOLAR_TO_BIPOLAR | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C1_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | |
| SOURCE_LFO | DEST_C2_OUTPUT_AMP | TRANSFORM_BIPOLAR_TO_BIPOLAR | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C2_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | dOscFoRange | |
| SOURCE_LFO | DEST_C3_OUTPUT_AMP | TRANSFORM_BIPOLAR_TO_BIPOLAR | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C3_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | dOscFoRange | |
| SOURCE_LFO | DEST_C4_OUTPUT_AMP | TRANSFORM_BIPOLAR_TO_BIPOLAR | FALSE |
| | dLFO1scModIntensity | m_DefaultRange | |
| SOURCE_LFO | DEST_C4_FO | TRANSFORM_NONE | FALSE |
| | dLFO1scModIntensity | dOscFoRange | |

Figure 12.16: One possible DXSynth GUI in RackKFX; notice that several controls are embedded in the LCD.

Figure 12.17: The DXSynth GUI for the VST3 and AU projects.

For a DX algorithm, the note event is only triggered when EGs on carrier operators have expired. In addition, legato mode and reset to zero are only applied to output EGs and not belongs to modulators, though you might experiment with this as well. We will be using the stock EGs that we have used in the previous projects for DXSynth, but if you want to be realistic, consider implementing an EG that closely matches the EG shown in Figure 12.18; not only this EG have five segments and different programming paradigms, the curve for the attack is different than any other states. See the Chapter Challenges for the exact operation of the EG.

Figure 12.18: Yamaha DX Envelope Generators have an additional segment and use LEVEL and RATE values for programming.

## 12.6 FM and PM in Oscillator Objects

The two oscillator objects WTOillator and CBLimOscillator are already designed and coded for FM and PM operation. First, both allow for positive or negative frequencies, as in Chapter 5. Next, both allow the instantaneous frequency or phase to change. We skipped over that previously, so's take a look at it now.

# FM

![](img/b42d0dca53f4a889d8162d55f7c8c05d_817_0.png)

we are ultimately designing a PM synth, but can still experiment with FM this today. The frequency modulation is calculated as an offset to the note frequency prior to this calc—we are literally changing the instantaneous frequency on each sample interval.

This code is inside the update() function:

You use the function setModLn() to set the linear frequency offset. To use this, you would multiply the output of the modulator by the frequency deviation value, which would scale the modulator to some positive and negative frequency offset.

```
// --- output of Op2*EG2 value
```

| Operator 1 | Attack | Decay | Sustain | Release | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Operator 2 | Attack | Decay | Sustain | Release | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Operator 3 | Attack | Decay | Sustain | Release | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Operator 4 | Attack | Decay | Sustain | Release | Feedback | Op21 | Op22 | Op23 | Op24 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | | | | | |

| Operator 1 | Attack | Decay | Sustain | Release | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Operator 2 | Attack | Decay | Sustain | Release | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Operator 3 | Attack | Decay | Sustain | Release | Output |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Operator 4 | Attack | Decay | Sustain | Release | Feedback |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 12.34 | 12.34 | 12.34 | 12.34 | 12.34 | |

| Voice | Portamento | Orde |
| :--- | :--- | :--- |
| DX1 | | |

| Global | Vel-At | Reset To | Legato | Filter Range |
| :--- | :--- | :--- | :--- | :--- |
| DFF | | | | |
| Note-Oct | | | | |
| GFF | | | | 12.34 |

| LFO | LFO Intensity | Opt21 | Opt22 | Opt23 |
| :--- | :--- | :--- | :--- | :--- |
| 0.5 | 12.34 | none | none | none |
