| Appendix B) | sendUpdateGUI() | updateDisplay() | N/A |
|---|---|---|---|
| Get the DLL's Directory | getMyDLLDirectory() | getDirectory() | N/A |
| Show a Custom GUI | showGUI() | dispatcher() | AudioUnitGetProperty() |

RackAFX, VST, and AU all provide for a default standard interface—a GUI that the user does not have to code. For RackAFX, you can optionally design your own custom GUI with the GUI designer (Appendix B) that requires no coding; alternatively, you can design your own (see Section A.1). VST and AU also allow you to design your own GUI. VST provides a GUI class of objects that you can optionally use in your coding that allows for cross-platform compatibility. AU only runs on Mac and does not provide cross-platform compatibility. The default interface setup for RackAFX involves you simply filling in a properties dialog for the components you want; the GUI object code is written for you. In VST and AU, you must set up a way to describe your controls. In all three formats, when you load your plug-in the client queries it for its default interface controls and then builds the GUI at run time. In RackAFX, the client simply iterates through your linked list of objects and sets up the GUI.

# A.4 VST Plug-in without Wrapping

Let's start by pretending to write a VST plug-in from scratch without wrapping any RackAFX code—of course, you can always cut and paste processing or cooking functions directly from your source, since it is pure C++. The pretend plug-in will be a delay with feedback called CDelay.

# A.4.1 Default GUI

First, you define an enumerated list of unsigned integer-type (UINT) constant values in your PlugIn.h file where “PlugIn” is the name and you have derived it from the AudioEffectX base class. These constants are the control ID values the host will use when querying about, getting, or setting a control variable. A delay plug-in might have delay time, feedback, and wet/dry mix controls, so you might define your enum as follows:

```
enum
{
   uDelayTime,    /* ID = 0 */
   uFeedBack,     /* ID = 1 */
   uWetDry,       /* ID = 2 */
   uNumParams     /* Always last = 3 = number of controls */
};
```

Next, you declare a parallel set of member variables that will be used in your plug-in. These are for cooked data values.

```
float m_fDelayTime;
float m_fFeedBack;
float m_fWetDry;
```

Finally, you declare the minimum and maximum values for each control.