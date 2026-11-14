
we should start by coding a module that can be used in larger parent plug-in objects. Figure 10.11 shows the block diagram.

We will provide several user interface (UI) components to control the plug-in and their variables are available for a parent plug-in to use as well. We will use the existing DDL module and wave table oscillator plug-ins. Since the DDL module has feedback path control, there will be many ways to combine these modules into sophisticated units. The controls we will provide for the user are discussed next. The plan of operation is as follows:

- LFO: needs to be set up to run unipolar and with the non-band-limited tables.
- The chorus delay offset control will effectively move the center of operation for the modulated delay.
- The vibrato mode will force the feedback value to 0.0% since it does not sound good with feedback.

- prepareForPlay()
  - Reset the LFO and start it by setting the m_bNoteOn flag; also set up the LFO and DDL modules.
  - Set the DDL m_nSampleRate variable; it needs this value to initialize its buffer properly.
  - Forward the prepareForPlay() call to the child objects, LFO and DDL.

![](img/b54974d0a4317ec82d7ae02126d10a6f_319_0.png)

Figure 10.11: Generic modulated delay block diagram; it can be any type of flanger/vibrato/chorus.

- processAudioFrame()
  - Call the doOscillate() function on the LFO.
  - Use the LFO value to calculate a delay offset in milliseconds for the DDL module.
  - Write the new delay time to the DDL module and call its cooking function.
  - Call processAudioFrame() on the DDL module to get the current output sample.

- userInterfaceChange()
  - Call the update functions for the LFO and DDL.
  - Call the type switching function to change from flanger to vibrato and chorus.

We'll go ahead and plan on some helper functions to make this process easier. This is not going to be the most streamlined or efficient code, but once you have it mastered you can always go back and improve it. Although this is a difficult project, you only need two member variables and four functions to accomplish the design.

The member objects are as follows:

```cpp
CWTOscillator m_LFO;    // our LFO
CDDLModule m_DDL;       // our delay line module
```

The member variables are as follows:

```cpp
float m_fMinDelay_mSec; // min delay time
float m_fMaxDelay_mSec; // max delay time
```

The member functions are as follows:

```cpp
float updateLFO();      // change/set the type and rate
float updateDDL();      // change/set the wet/dry and feedback
float cookModType();    // set up the min/max delay times
float calculateDelayOffset(float fLFOSample); // convert the LFO to a delay value
```

## 10.3.1 Project: ModDelayModule

Start a new project and make sure to include your WTOScillator and DDLModule objects (Figure 10.12).

![](img/b54974d0a4317ec82d7ae02126d10a6f_320_0.png)

Figure 10.12: Project settings for the ModDelayModule.

Table 10.2: The GUI components, variable names, and values.

| Slider Property | Value |
|---|---|
| Control Name | Depth |
| Units | % |
| Variable Type | float |
| Variable Name | m_fModDepth_pct |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 50 |

| Slider Property | Value |
|---|---|
| Control Name | Rate |
| Units | Hz |
| Variable Type | float |
| Variable Name | m_fModFrequency_Hz |
| Low Limit | 0.02 |
| High Limit | 5 |
| Initial Value | 0.18 |

| Slider Property | Value |
|---|---|
| Control Name | Feedback |
| Units | % |
| Variable Type | float |
| Variable Name | m_fFeedback_pct |
| Low Limit | -100 |
| High Limit | 100 |
| Initial Value | 0 |

| Slider Property | Value |
|---|---|
| Control Name | Chorus Offset |
| Units | mSec |
| Variable Type | float |
| Variable Name | m_fChorusOffset |
| Low Limit | 0 |
| High Limit | 30 |
| Initial Value | 0 |

| Button Property | Value |
|---|---|
| Control Name | Mod Type |
| Units | |
| Variable Type | enum |
| Variable Name | m_uModType |
| Enum String | Flanger, Vibrato, Chorus |

| Button Property | Value |
|---|---|
| Control Name | LFO |
| Units | |
| Variable Type | enum |
| Variable Name | m_uLFOType |
| Enum String | tri, sin |

Set up the graphical user interface (GUI) in RackAFX with Table 10.2.

## 10.3.3 ModDelayModule.h File

Add the member objects, variables, and function declarations to the .h file:

```cpp
// Add your code here: ------------------------------------------------------ //
CWTOscillator m_LFO; // our LFO
CDDLModule m_DDL; // our delay line module

// these will depend on the type of mod
float m_fMinDelay_mSec;
float m_fMaxDelay_mSec;

// functions to update the member objects
void updateLFO();
void updateDDL();

// cooking function for mod type
void cookModType();

// convert a LFO value to a delay offset value
float calculateDelayOffset(float fLFOSample);

// END OF USER CODE ------------------------------------------------------- //
```

## 10.3.4 ModDelayModule.cpp File

### Constructor

- Initialize all variables.

```cpp
CModDelayModule::CModDelayModule()
{
	<SNIP SNIP SNIP>

	// Finish initializations here
	m_fMinDelay_mSec = 0.0;
	m_fMaxDelay_mSec = 0.0;
	m_fChorusOffset = 0.0;

	m_LFO.m_fFrequency_Hz = 0;
	m_LFO.m_uOscType = m_uLFOType; // triangle enum(tri,sin);

	m_DDL.m_bUseExternalFeedback = false;
	m_DDL.m_fDelay_ms = 0;
}
```

Write the update() functions:

```cpp
// LFO function to set:
// - the LFO Frequency
// - the oscillator type
void CModDelayModule::updateLFO()
{
    // set raw data
    m_LFO.m_fFrequency_Hz = m_fModFrequency_Hz;
    m_LFO.m_uOscType = m_uLFOType;

    // cook it
    m_LFO.cookFrequency();
}

// DDL function to set:
// - the DDL Feedback amount (disabled for Vibrato)
void CModDelayModule::updateDDL()
{
    // test and set if needed
    //if(m_uModType != Vibrato)
    m_DDL.m_fFeedback_pct = m_fFeedback_pct;

    // cook it
    m_DDL.cookVariables();
}
```

Write the cookModType() function using the information in Table 10.3—this method is called when the user changes the effect type.

| Effect | Min Delay (mSec) | Max Delay (mSec) | Wet/Dry(%) | Feedback(%) |
|---|---|---|---|---|
| Vibrato | 0 | 7-10 | 50/50 | -100 to +100 |
| Chorus | 5 | 20-40 | 50/50 | -100 to +100 |

```cpp
void CModDelayModule::cookModType()
{
    switch(m_uModType)
    {
        case Flanger:
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fFeedback_pct = m_fFeedback_pct;
            break;
        }
        case Vibrato:
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 100.0;
            m_DDL.m_fFeedback_pct = 0.0; // NOTE! no FB for vibrato
        }
        case Chorus:
        {
            m_fMinDelay_mSec = 5;
            m_fMaxDelay_mSec = 30;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fInputAttenuation = 1.0;
            break;
        }
        default: // is Flanger
        {
            m_fMinDelay_mSec = 0;
            m_fMaxDelay_mSec = 7;
            m_DDL.m_fWetLevel_pct = 50.0;
            m_DDL.m_fFeedback_pct = m_fFeedback_pct;
            break;
        }
    }
}
```

Table 10.3: The default delay line settings for the various effects.

| | Min Delay(mSec) | Max Delay(mSec) | Wet/Dry(%) | Feedback(%) |
|---|---|---|---|---|
| Flanger | 0 | 7-10 | 50/50 | -100 to +100 |
| Vibrato | 0 | 7-10 | 100/0 | 0 |
| Chorus | 7 | 20-40 | 50/50 | Typically 0 |

Write the calculateDelayOffset() function. It works by taking the LFO value from 0 to 1.0 and mapping it on to the range from min to max delay. Then, this value is scaled by the depth percent value so that at 100% the maximum range is used. For the chorus, we effectively move the operating range and chorus center by adding a delay offset to the minimum value, then using that as the starting (reference) point in the calculation.

```cpp
// calculateDelayOffset():
/*
 fLFOSample: a value from 0.0 to 1.0 from the LFO object

 returns: the calculated delay time in mSec for each effect

 NOTES: - the range for the flanger/vibrato is simply mapped from min to max
         starting at min: fLFOSample*(m_fMaxDelay_mSec - m_fMinDelay_mSec) +
         m_fMinDelay_mSec
     
     - the range for the Chorus includes the starting offset
        fStart = m_fMinDelay_mSec + m_fChorusOffset;
*/
if(m_uModType == Flanger || m_uModType == Vibrato)
{
  // flanger 0-1 gets mapped to 0->maxdelay
  return (m_fModDepth_pct/100.0)*(fLFOSample*(m_fMaxDelay_mSec -
  m_fMinDelay_mSec)) + m_fMinDelay_mSec;
}
else if(m_uModType == Chorus)
{
  // chorus adds starting offset to move delay range
  float fStart = m_fMinDelay_mSec + m_fChorusOffset;
  return (m_fModDepth_pct/100.0)*(fLFOSample*(m_fMaxDelay_mSec -
  m_fMinDelay_mSec)) + fStart;
}
```

## 10.3.5 PrepareForPlay()

- Forward the call to prepareForPlay() on the member objects.
- Reset and start up the LFO in unipolar mode.
