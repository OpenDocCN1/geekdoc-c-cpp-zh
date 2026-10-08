
```cpp
OSStatus AUSynth::Render(args...)
{
    // --- broadcast MIDI events
    PerformEvents(inTimestamp);

    <SNIP SNIP SNIP>
    // --- the frame processing loop
    for(Uint32 frame=0; frame<inNumberFrames; ++frame)
    {
        // --- clear accumulators
        dOutL = 0.0;
        dOutR = 0.0;
        if(m_oscl1.bNoteOn)
        {
            << INSERT ** Code Listing 7.1: Audio Rendering ** HERE >>
        }
        // write out to buffer
        // --- mono
        left[frame] = dOutL;
    }

    etc...
}
```

## Chapter 8
Parameterization

The NanoSynth project is taking shape, but there are problems that need to be fixed and flexibility that needs to be added. First, NanoSynth is hard-wired into a specific configuration or patch. For example, the user can't re-route the LFO from the oscillators to some other destination such as the filter cutoff frequency. And, each time we design a new synth architecture, we will have to manually connect the components by wiring the code. Second, it is monophonic, and we would like to make polyphonic synthesizers (or at least understand). In this chapter, we will address the first issue with a modulation matrix that is programmed with a patch configuration as a series of rows in the matrix. This will allow the user more control over modulation routings as well simplify the coding for the render function. Next, we will use the standard MIDI controller modulations that all the projects will contain. Then, we will add another note of polyphony to the synth and experiment with voice-stealing in the two-note NanoSynth Poly. Finally, we will use global parameterization to streamline the synth updating process. We are going to try to add these new features to NanoSynth in the most easy-to-understand manner as possible. In the next chapter, however, we will address some of the issues that arise and modify the paradigm slightly—NanoSynth is our "learning synth," and we will be using experience to help mold the future projects. This is an important chapter—since the rest of the projects use the same core MIDI functionality, modulation matrix concepts and global parameterization, this is the last time we will print the details of the synth-plugin details.

You are strongly urged to obtain the MIDI Manufacturers Association DLS Level II Specification. It is the spec for a software that uses audio samples in oscillators. More importantly, it is the modulation concept on which this chapter is based. It also includes a set of GUI and object min, max and default values, an alternate and interesting filter design, and copious information on the sample-based synthesis. Finally, it is an actual specification intended for major synth manufactures to use. Unless you work at a synth company, this is the closest you will come to seeing an actual synth specification.

### 8.1 Modulation Routings

Figure 8.1 shows the block diagram for NanoSynth so far. The modulation routings are in dotted lines. You can make some observations:

- the EG1 to Oscillator and EG1 to DCA routings have intensity controls that alter their modulation amounts
- the LFO to Oscillator and EG1 to Filter routings do not have these controls
- the LFO intensity is globally controlled with its amplitude variable
- the EG and LFO outputs are summed before applying to the Oscillator fo modulation
- there is no control between EG1 and the filter cutoff
- there are no switches that can re-route modulation outputs
- there are no switches that enable disable routings

In this chapter, we will learn how to set up a modulation matrix both with and without the intensity controls in which multiple modulation sources can feed modulation destinations in a highly flexible way. It will be easy for to add your own custom sources and destinations. You will also learn how to enable or disable routings in the matrix. Figure 8.1 shows the detailed connection graph for NanoSynth so far. The dotted lines show the modulation routings.

Let's list the modulation sources and destinations in Figure 8.1 by tracing the dotted line connections.

Sources:

- EG1 output
- EG1 biased output
- LFO1 output
- MIDI Note Number (for filter key-track modulation)

![](img/b42d0dca53f4a889d8162d55f7c8c05d_457_0.png)

Figure 8.1: The detailed NanoSynth block diagram.

Destinations:

- Osc1 $f_0$ Mod
- Osc2 $f_0$ Mod
- Filter $f_c$ Mod

### DCA EG Mod

There are more possible sources and destinations, and in this chapter we will add several of them. Figure 8.2 shows a conceptual diagram of the modulation routings in the current version of NanoSynth. The sources are lined up with the leftist destinations on the right. We see instances where one source feeds multiple destinations and where one destination's intensity is the sum of multiple sources. We want to describe the modulation matrix with this kind of flexibility built-in and no limit to the number of routings.

Now, think about how the code looks when rendering the audio. For the EG to Oscillator Fo routing, the final modulation value is the product of the intensity, range and modulation output:

```cpp
double dEG0scMod =
m_dEG0scIntensity_OSC_FO_MOD_RANGE*dBiasedEG;
```

Next, the LFO1 routing, the final modulation value is the product of the intensity, range and modulation output:

```cpp
double dLFO1scMod =
m_dLFO1scIntensity_OSC_FO_MOD_RANGE*dLFO1;
```

The EG to DCA routing, the final modulation value is the product of the intensity, range and modulation output:

```cpp
double dEGDCAMod =
m_dEGDCAIntensity_DCA_MOD_RANGE*dBiasedEG;
```

The EG to Filter routing, the final modulation value is the product of the intensity, range and modulation output:

```cpp
double dEGFilterMod =
m_dEGFilterIntensity_FILTER_MOD_RANGE*dBiasedEG;
```

The MIDI to Filter routing, the final modulation value is the product of the intensity, range and modulation output:

```cpp
double dMIDIFilterMod =
m_dMIDIFilterIntensity_FILTER_MOD_RANGE*dMIDINoteNumber;
```

| Source | Transform | Intensity | Destination |
| :--- | :--- | :--- | :--- |
| LFO1 Output | none | 1.0 | Osc1 Fo Mod |
| LFO1 Output | none | 1.0 | Osc2 Fo Mod |
| LFO1 Output | none | 1.0 | Filter Fc Mod |
| EG1 Output | none | 1.0 | Osc1 Fo Mod |
| EG1 Output | none | 1.0 | Osc2 Fo Mod |
| EG1 Output | none | 1.0 | Filter Fc Mod |
| EG1 Biased Output | none | 1.0 | Osc1 Fo Mod |
| EG1 Biased Output | none | 1.0 | Osc2 Fo Mod |
| EG1 Biased Output | none | 1.0 | Filter Fc Mod |
| MIDI Note Number | none | 1.0 | Osc1 Fo Mod |
| MIDI Note Number | none | 1.0 | Osc2 Fo Mod |
| MIDI Note Number | none | 1.0 | Filter Fc Mod |

Figure 8.2: The modulation routings.

### 8.2 The Modulation Matrix

Here is the idea behind the modulation matrix: currently, you have to write the code that takes the modulation outputs from the LFO, EG and the MIDI Note Number, scale them by range and intensity. This chapter, we will learn how to set up a modulation matrix both with and without the intensity controls in which multiple modulation sources can feed modulation destinations in a highly flexible way. It will be easy for to add your own custom sources and destinations. You will also learn how to enable or disable routings in the matrix. Figure 8.1 shows the detailed connection graph for NanoSynth so far. The dotted lines show the modulation routings.

| Source | Transform | Intensity | Destination |
| :--- | :--- | :--- | :--- |
| LFO1 Output | none | 1.0 | Osc1 Fo Mod |
| LFO1 Output | none | 1.0 | Osc2 Fo Mod |
| LFO1 Output | none | 1.0 | Filter Fc Mod |
| EG1 Output | none | 1.0 | Osc1 Fo Mod |
| EG1 Output | none | 1.0 | Osc2 Fo Mod |
| EG1 Output | none | 1.0 | Filter Fc Mod |
| EG1 Biased Output | none | 1.0 | Osc1 Fo Mod |
| EG1 Biased Output | none | 1.0 | Osc2 Fo Mod |
| EG1 Biased Output | none | 1.0 | Filter Fc Mod |
| MIDI Note Number | none | 1.0 | Osc1 Fo Mod |
| MIDI Note Number | none | 1.0 | Osc2 Fo Mod |
| MIDI Note Number | none | 1.0 | Filter Fc Mod |

Figure 8.2: The modulation routings.

Each of the individual routings occupies one row in the table.

Here is the idea behind the modulation matrix: currently, you have to write the code that takes the modulation outputs from the LFO, EG and the MIDI Note Number, scale them by range and intensity.
