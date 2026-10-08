have a completely different contour. Allow the user to choose between EG1 (classic mode) and EG2 for the filter

```
// initialize the controls here!
// -- these are defined in SynthParamLimits.h
```

```
Globals()->SetParameter(NOISE_OSC_AMP_DB, DEFAULT_NOISE_OSC_AMP_DB);
Globals()->SetParameter(PULSE_WIDTH_PCT, DEFAULT_PULSE_WIDTH_PCT);
```

<SNIP SNIP SNIP>

```
<< INSERT ** Code Listing 9.2: Init Voices ** >>
```

```
}
```

EG.

```
AUSynth::AUSynth(void)
```

Platinum
{
			<< INSERT ** Code Listing 9.3: Destruction ** HERE **

Implement MiniSynth mklIII shown in Figure 9.15. This version adds a second LFO in a

```
ComponentResult AUSynth::Reset(args. ..)
{
			// -- reset the base class
	
AUBase::Reset(inScope, inElement);
```

```
<< INSERT ** Code Listing 9.4: One Time Init ** >>
```

```
return noErr;
```

```
}
```

```
ComponentResult AUSynth::Initialize())
{
			// -- init the base class
	AUInstrumentBase::Initialize();
```

```
<< INSERT ** Code Listing 9.4: One Time Init ** >>
```

```
return noErr;
```

```
}
```

```
OSStatus AUSynth::Render(args. ..)
{
```