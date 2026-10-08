In Visual Studio, select the MiniSynth.h file and scroll to the bottom to see all the variables that were added when set up the GUI. Notice the combination of doubles, ints, UINTs and enums. For example, the UINT m_uVoiceMode uses the enum list just below it to show the user possible Voice settings.

```
class CMiniSynth : public CPlugin
{
public:
    // RackAFX plug-in API Member Methods:

<SNIP SNIP SNIP>

// ADDED BY RACKFX -- DO NOT EDIT THIS CODE!!!
// **--0x07FD--**

UINT m_uVoiceMode;
enum(Saw3,Sqr3,Saw2Sqr,Tri2Saw,Tri2Sqr);
double m_dDetune_cents;
double m_dFCcControl;
double m_dLF01Rate;
etc...

// **--0x1A7F--**
//
```

Now, focus on the member functions at the top of the file. We will be overriding and/or implementing the CPlugin functions for our synth projects:

Standard plug-in
Functions:

Here you see the constructor and destructor, which we use to initialize variables and destroy objects.