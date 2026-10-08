
```cpp
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

```cpp
m_vpg.setVpgStep(1, 0.0, 1.0, 2000, false);
m_VPG.setProgramStep(2, 1.0, 0.0, 2000, true);
m_VPG.setProgramStep(3, 0.0, -1.0, 2000, true);
```

```cpp
// --- RAFX version, VPG is disabled so you can use the easy
// programJoystick in RAFX (hit the Program button)
m_bEnableVPG = false;
// m_bEnableVPG = true; <-- uncomment to use VPG instead of JSProgram

#else
// -- the flag means you used rotated coordinates
m_VPG.setProgramStep(0, -1.0, 1.0, 2000, false);

m_VPG.setProgramStep(1, 1.0, 1.0, 2000, false);
m_VPG.setProgramStep(2, 1.0, -1.0, 2000, false);
m_VPG.setProgramStep(3, -1.0, -1.0, 2000, false);

// --- for VST/AU, there is no built-in generator, do it by
// hand
m_bEnableVPG = true;
#endif
```

initializations. You need to update the new global parameters here where you simply parse the variables off your global parameter structure.

reset()
In reset() you just call the base function.

noteOn()
In noteOn() you need to add a call to start the vector path generator or RAFX joystick program; the path is executed for each note that is played. This is done after calling the base implementation. Notice the use of the m_bEnableVPG flag and checking of the JSProgram pointer prior to calling the start() function.

noteOff()
In noteOff() you need to add a call to resume the vector path generator or RAFX joystick program in sustain mode since these objects will halt at the second-to-last vertex during the sustain portion of the event.

```cpp
inline virtual void initGlobalParameters(GlobalParams* pGlobalParameters)
{
// --- always call base class
// ---
// add any CVectorVoice specific variables here (you need to add them to the global struct)
m_pGlobalParams->dOrbitXAmp = m_dOrbitXAmp;
m_pGlobalParams->dOrbitYAmp = m_dOrbitYAmp;
m_pGlobalParams->uVectorMode = m_uVectorMode;

m_pGlobalParams->dAmplitude_A = m_dAmplitude_A;
m_pGlobalParams->dAmplitude_B = m_dAmplitude_B;
m_pGlobalParams->dAmplitude_C = m_dAmplitude_C;
m_pGlobalParams->dAmplitude_D = m_dAmplitude_D;

m_pGlobalParams->dAmplitude_ACmix = m_dAmplitude_ACmix;
m_pGlobalParams->dAmplitude_BDmix = m_dAmplitude_BDmix;
}
```

```cpp
void CVectorSynth::initializeModMatrix(ModulationMatrix* pMatrix)
{
// --- always first: call base class to create core and init with basic routing
CDigiSynthVoice::initializeModMatrix(pMatrix);

if(!pMatrix->getModMatrixCore()) return;

MatrixRow* pRow = NULL;

// --- vs uses LFO2 as "Rotor"
// LFO2 -> VS AC Mod

doVoice()
This is the most important function of all since it does the rendering, and it is nearly identical to DigiSynth. The modulation layers are the same, however you need to deal with the vector mix component and the new Rotor LFO2.

The differences from DigiSynth are shown in bold. The vector synth implementation requires a call to the function:

```cpp
pRow = createMatrixRow(SOURCE_LF02, DEST_VS_AC_AXIS, &m_dModIntensity, &m_dDefaultModRange, true);
pMatrix->addMatrixRow(pRow);
```

```cpp
// LF02Quad -> VS Axis Mod
pRow = createMatrixRow(SOURCE_LF02Q, DEST_VS_BD_AXIS, &m_dModIntensity, &m_dDefaultModRange, true);
pMatrix->addMatrixRow(pRow);
```

```cpp
void CVectorSynth::setSampleRate(double собствеRate)
{
CDigiSynthVoice::setSampleRate(dSampleRate);

// --- all APIs have access to m_VPG
m_VPG.setSampleRate((float)dSampleRate);

// --- RackAFX only
if(m_pJSProgram)
    m_pJSProgram->setSampleRate((int)dSampleRate);
```

calculateVectorMixValues(), which takes into account all possible modulations—the path, rotor and joystick-center-of-operation—and produces the vector mix components for the current sample period.

```cpp
void calculateVectorMixValues(double dOriginX, double dOriginY,
double dPointX, double dPointY,
double& dAmag, double& dBMag, double& dCMag, double& dDMag,
double& dACMix, double& dBBMix;
```

```cpp
void CVectorSynth::preparePlay()
{
  CDigiSynthVoice::preparePlay();
}
```

```cpp
void CVectorSynth::update()
{
  // --- voice specific updates
  if(!m_pGlobalVoiceParams) return;
}
```

int nCellsPerSide, bool bJoystickCoords = true)

The arguments are:

```cpp
// --- call base class
CDigiSynthVoice::update();
```

```cpp
// --- VS Specific
// --- path mode
m_uvectorPathMode = m_pGlobalVoiceParams->uVectorPathMode;
```

```cpp
// --- for RAFX
if(m_pJSProgram)
    m_pJSProgram->setJSMode(m_uvectorPathMode);
```

```cpp
// --- for everyone else (or RAFX)
m_VPG.setVPGPathMode(m_uVectorPathMode);

// --- joystick params
m_dAmplitude_A = m_pGlobalVoiceParams->dAmplitude_A;
m_dAmplitude_B = m_pGlobalVoiceParams->dAmplitude_B;
m_dAmplitude_C = m_pGlobalVoiceParams->dAmplitude_C;
m_dAmplitude_D = m_pGlobalVoiceParams->dAmplitude_D;
m_dAmplitude_ACmix = m_pGlobalVoiceParams->dAmplitude_ACmix;
m_dAmplitude_BDmix = m_pGlobalVoiceParams->dAmplitude_BDmix;
```

+   #include "VectorSynth.h" at the top of the file

```cpp
void CVectorsSynth::reset() {

  CDigiSynthVoice::reset();
}
```

# Loading Samples

The code for loading samples is slightly different from
- the loadsSamples() function is carryover from DigiSynth
```
