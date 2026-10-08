```
// -- init false, false = NOT single-sample,
// NOT pitchless sample
m_pVoiceArray[i]->initAll10scWithDigiSynthVoice(m_pVoiceArray[0],
    false, false);

// always delete what comes back from addStrings()
delete [] pPath0;
delete [] pPath1;
delete [] pPath2;
delete [] pPath3;

// --- VST3 only
delete [] pDLLPath;

// --- AU only
delete [] componentFolder;

<< END ** Code Listing 11.2: Load Samples ** END >>

class CVectorSynth : public CPlugin
{
public:
    <SNIP SNIP SNIP>

    // Add your code here: --------------------

<< INSERT ** Code Listing 11.1: Declarations ** HERE >>
```

etc...

+   * Initialize()