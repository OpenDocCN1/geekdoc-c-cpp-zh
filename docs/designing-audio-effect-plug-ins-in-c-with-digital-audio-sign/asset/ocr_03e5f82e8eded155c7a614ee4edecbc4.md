# 3.9.4 Volume.h File

Before we add the code, look around the plug-in object files (volume.h and volume.cpp) to get a better understanding of what's going on and what you'll need to modify. First, open the volume.h file and look inside:

```
// RackAFX abstract base class for DSP filters
class CVolume : public CPlugIn
{
public: // plug-in API Functions
//
// 1. One Time Initialization
CVolume();
<SNIP SNIP SNIP>
// 7. userInterfaceChange() occurs when the user moves a control.
virtual bool userInterfaceChange(int nControlIndex);
// Add your code here: ------------------------------------------ //
// END OF USER CODE --------------------------------------------- //
// ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!! ----------------- //
// ****--0x07FD--****
float m_fVolume;
// ****--0x1A7F--****
// -------------------------------------------------------------- //
};
```

Aside from the main plug-in functions we discussed in Chapter 2, you will see some more commented areas of code. In the first part marked // Add your code here: you can add more variables or function definitions just like you would in any .h file. Try to keep your code in the denoted area to make it easier to find and read. The area below that says:

> // ADDED BY RACKAFX—DO NOT EDIT THIS CODE!!!

is very important—you will see your member variable m_fVolume declared in this area. This is the portion of the .h file that RackAFX modifies when you add, edit, or delete controls from your control surface. It is imperative that you let RackAFX maintain this part of the C++ code. There are several other portions of code in the .cpp file that have similar warnings and interesting hex symbols (0x1A7F, etc.); do not edit the code contained between the hex codes or commented areas.

> You will see the notation <SNIP SNIP SNIP> frequently in the printed code as a reminder that code has been cut out for easier reading.

> RackAFX writes C++ code for you! But, you have to be careful not to alter the RackAFX C++ code in any way. You can always tell if the code is RackAFX code because there will be warning comments and strange hex codes surrounding the RackAFX code. The RackAFX code is left for you to see only as a backup to your debugging and should never be altered by anyone except RackAFX.