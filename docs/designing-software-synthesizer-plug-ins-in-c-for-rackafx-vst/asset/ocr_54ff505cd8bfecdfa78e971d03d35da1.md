```
double lF01doOut = m_LF01.dooscillate();
double DEGOut = m_EG1.doEnvelope();
```

```
m_Osc1.setFoModExp(dLF01doOut*OSC_FO_MOD_RANGE);
m_Osc2.setFoModExp(dLF01doOut*OSC_FO_MOD_RANGE);
m_Osc1.update();
m_Osc2.update();
```

```
m_DCA.setEGMod(DEGOut*m_EG1DCAIntensity);
m_DCA.update();
```

```
// --- DIGITAL AUDIO ENGINE BLOCK --/
// (OSC1 + OSC2) --> DCA
double d0scout = 0.5*m_osc1.dooscillate() + 0.5*m_osc2.dooscillate();
```

```
// now process through DCA
m_DCA.doDCA(d0scout, d0scout, dOutL, dOutR);
```

```
// now check for note off
if(m_EG1.getState() == 0) 0 = off
```

+   - update the EG and DCA with the GUI control variables
- there is no reason yet to call the update function on the EG; we will add this in Chapter 8

```
m_Osc1.stoposcillator();
m_Osc2.stoposcillator();
m_LF01.stoposcillator();
m_EG1.stopEG();
```

> << END ** Code Listing 6.1: Rendering Audio ** END >>

# process()

+   - modify the audio rendering code

doProcessEvent()