# AU;

getMyComponentDirectory().
globally declared at the top of
AUSynth.

```
double CsOscillator::dooscillate(double* pAxOutput)

// -- clear in case of no sample
m_dleftOutputSample = 0.0;
m_dRightOutputSample = 0.0;
if(pAxOutput)*pAxOutput = 0.0;
```

# Simple-Sample Example

Here is an example of initializing a
CsampleOscillator with a single-
sample called FuzzVibeA1.wav in
e plug-in API. Individual
samples are in a directory called
Samples.

```
// -- get the sample pointer
WaveData* pSample = m_pWaveSample;
if(pSample)

pSample = m_pWaveSamplePtrArray[m_uUMIDNotNumber];
```

# RackAFX

Notice the use of addStrings()
helper; this is the same one you
learned in Chapter 3
we logged MIDI events with the
status window. You must always
delete the string that addStrings()
returns.

```
// -- check and bail if sample loaded
if(pSample) || !mbNoteOn
return 0.0;

// -- one-shot sample
if(m_dReadIndex < 0)
return 0.0;
```

```
// -- get
path
```

```
// -- do the buffer operation
readBuffer(pSample, m_dReadIndex, m_dInc.
m_dLeftOutputSample, m_dRightOutputSample;
```

char* pPath =
addSprite(getMyDLLDirectory(),"\\Samples\\FuzzVibeA1.wav");

```
// -- channel count
double dChannels = (double)pSample->m_uNumChannels;

// -- check for wrap
if(pSample->m_uLoopCount > 0)

// -- use loop points for looping
if(m_uLoopMode -- sustain)
```

# VST3

In VST3, the function requires you to pass the name of the plug-in's DLL file, then you use addStrings() like
RackAFX. You must always delete the string that addStrings() returns.

```
// -- get
path
char* pPath =
getMyDLLDirectory(USTRING("DigiSynth.vst3"));
```