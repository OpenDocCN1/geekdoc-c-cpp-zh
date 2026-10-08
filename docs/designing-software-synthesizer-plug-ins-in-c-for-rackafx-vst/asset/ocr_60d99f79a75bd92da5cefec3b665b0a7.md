matrix and update the components that were modulated. Then, the digital audio engine processing can happen.
// -- these are modulators: they write their outputs into

```
The code for rendering the audio is in Code Listing 8.3—this identical block of code is used on all three platforms.
m_LF01.m_pModulationMatrix = &m_ModulationMatrix;
m_LF01.m_uModDestOutput1 = SOURCE_LF01;
m_LF01.m_uModDestOutput2 = SOURCE_LF01Q;
```

```
m_EG1.m_pModulationMatrix = &m_ModulationMatrix;
m_EG1.m_uModDestEGOutput = SOURCE_EG1;
m_EG1.m_uModDestBiasedEGOutput = SOURCE_BIASED_EG1;
```

Now, let's complete the rest of the new NanoSynth MM1 (Mod Matrix 1) project—you can start a new project or keep modifying your existing NanoSynth. You can also download the NanoSynth MM1 project.

```
// -- DCA Setup:
m_DCA.m_pModulationMatrix = &m_ModulationMatrix;
m_DCA.m_uModSourceEG = DEST_DCA_EG;
m_DCA.m_uModSourceAmp_dB = DEST_NONE; // not connected (yet)
m_DCA.m_uModSourceVelocity = DEST_NONE; // not connected (yet)
m_DCA.m_uModSourcePan = DEST_NONE; // not connected (yet)
```

# << END ** Code Listing 8.2: Mod Matrix Connections I ** END >>

```
// -- mod matrix stuff
if(m_uFilterKeyRow == 1)
m_GlobalModMatrix.enableModMatrixRow(SOURCE_MIDI_NOTE_NUM,
DEST_ALL_FILTER_KEYTRACK, true);
```

else

```
m_GlobalModMatrix.enableModMatrixRow(SOURCE_MIDI_NOTE_NUM,
DEST_ALL_FILTER_KEYTRACK, false);
```

# NanoSynth MM Part One: RackAFX

# << ** Code Listing 8.3: Mod Matrix Renderer I ** >>

Copy the ModulationMatrix.h and .cpp files into your project folder and add them into the Visual Studio project.

```
// -- ARTICULATION BLOCK -- /
// -- DO layer 0 modulators
m_GlobalModMatrix.doModulationMatrix(0);
```

```
// -- update layer 1 modulators
m_EG1.update();
```

8.4