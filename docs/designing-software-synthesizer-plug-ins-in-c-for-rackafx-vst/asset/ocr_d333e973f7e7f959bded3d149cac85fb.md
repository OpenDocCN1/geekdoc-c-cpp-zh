clear the modulation variables

# update()

```
// --- called during updates
inline void setAttackTime_mSec(double d)
{
    m_dAttackTime_mSec = d;
    calculateAttackTime();
}
```

+   - recalculates the gain variable
- notice it is a combination of all modulation inputs and MIDI control values
- uses the midiToAtten() function supplied in synthfunctions.h to use the convex transform, you can feel free to change this to any kind of amplitude curve you wish

```
inline void setDecayTime_mSec(double d)
{
    m_dDecayTime_mSec = d;
    calculateDecayTime();
}
```

# DCA()

+   - calculate total pan value as a sum of controls and modulation
- limit the pan values to [-1..+1] in case there is a bias due to user's control setting
- calculate equal power pan values
- form left right outputs from a combination of gain and panning values
- use pass-reference to pass output values; always acts in stereo, even if no right input exists

```
inline void setReleaseTime_mSec(double d)
{
    m_dReleaseTime_mSec = d;
    calculateReleaseTime();
}
```

```
inline void setSustainLevel(double d)
{
    m_dSustainLevel = d;
    // --- sustain level affects decay
    calculateDecayTime();
}
```

# 6.14 NanoSynth: EG/DCA

```
// --- and release, if not in release state
if(m_uState != )
    calculateReleaseTime();
```

We continue with our learning-synth that we modified in the last chapter. In this chapter, we will add an envelope generator and DCA. Figure 6.30 shows the simplified block diagram for NanoSynth with the EG and DCA added. For this chapter we will use only the EG as an output on the DCA. In subsequent chapters we will use it to modulate the oscillators and filters.

You can use the NanoSynth plug to test the functionality of the objects and extend them with the Chapter Challenges. Table 6.3 shows the continuous and enumerated list GUI controls you need to add to the existing NanoSynth project. You might want to look at the sample code, then try your own implementation. Remember, it is up to you to design, code and manage your GUI on your platform of choice. Refer back to Chapter 2 of the