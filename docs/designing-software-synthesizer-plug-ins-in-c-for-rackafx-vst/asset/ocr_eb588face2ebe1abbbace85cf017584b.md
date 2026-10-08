```
// --- for voice stealing
m_EG1.m_bResetToZero = true;

// --- experiment with NLP
m_LeftK35Filter.m_nULP = ON;
m_RightK35Filter.m_nULP = ON;

// m_EG1.setEGMode(analog);
m_EG1.m_bOutputEG = true;

// --- VS Specific
m_dAmplitude_A = 0.25;
m_dAmplitude_B = 0.25;
m_dAmplitude_C = 0.25;
m_dAmplitude_D = 0.25;
m_dAmplitude_ACmix = 0.5;
m_dAmplitude_BDmix = 0.5;
m_dVectorCenterX = 0.0;
m_dVectorCenterY = 0.0;
m_dOrbitXAmp = 0.0;
m_dOrbitYAmp = 0.0;

// --- plug-in must set this RAFX only!!
m_pJSProgram = NULL;
m_uVoiceMode = manual;

// // example of programmatically creating a vector path
// without RAFX program generator

// -- Setup vector path generator; this just moves around from
// one apex to the next.

// start at 100% A morph to next step in 2 sec
// start at 100% B morph to next step in 2 sec
// start at 100% C morph to next step in 2 sec
// start at 100% D morph to BEGINNING in 2 sec (if LOOP mode)

#ifdef _RAFX
// the true argument means using Korg/RAFX coordinates
m_VPG.setProgramStep(0, -1.0, 0.0, 2000, true);
```

first, then do any voice specific