
# MIDI Functions

| MIDI Message | RackAFX | VST3 | AU |
|---|---|---|---|
| Pitch Bend | midiPitchBend() | process() | HandlePitchWheel() |
| Mod Wheel | midiModWheel() | process() | HandleControlChange() |
| All other MIDI Messages | midiMessage() | process() | HandleControlChange() HandleMidiEvent() |

Table 2.4: GUI functions for RackAFX, VST3 and AU.

| GUI Set and Maintenance | RackAFX | VST3 | AU |
|---|---|---|---|
| Declare/Describe Controls, set limits and defaults | done with an easy use Control Designer—you fill in a parameter that synthesizes the code for you | you must write the code yourself | you must write the code yourself |
| Initialize Controls | automatically written for you | you must write the code in initialize() | you must write the code in initialize() GetParameterInfo() GetParameterString() |
| Write control values to file (presets) | automatically written for you | you must write the code in getState() | automatically written for you |
| Read control values from file (presets) | automatically written for you | you must write the code in setState() | automatically written for you |
| Declare/Create GUI | automatically written for you | you must write the code in createView() | GUI Class Factory that you design and write |
| Graphical Design of GUI | Drag-And-Drop GUI built into RackAFX | Drag-And-Drop GUI via the VST3 Host | InterfaceBuilder in XCode |

Table 2.5: Comparison of the three platforms in this book.

| Platform | Pros | Cons |
|---|---|---|
| RackAFX | - simplest API with very few files and no GUI programming<br>- RackAFX writes some of the code for you<br>- supports multiple Visual Studio compilers including the free Expressions<br>- runs with very little system overhead for good polyphony count<br>- highly portable projects that do not require a specific folder hierarchy<br>- debug through RackAFX itself<br>- Vector Joystick programmer is built-in | - only runs in Windows<br>- for ported projects you must write and maintain your own GUI; can't drag-and-drop editor<br>- GUI controls are limited (fixed number of bitmap options, can not add your own graphics files) |
| VST3 | - virtually identical code for Windows and macOS versions (though this book only covers the Windows version)<br>- can use VSTGUI library and editor for reasonably simple GUI design<br>- VSTGUI allows you to customize your own GUI controls with skins/bitmaps<br>- VSTGUI includes many types of controls<br>- highly flexible and safe thanks to Com implementation | - most complicated API<br>- requires knowledge of Microsoft's Common Object Model (COM)<br>- large number of supporting files to maintain<br>- SDK creates a directory hierarchy that is difficult to modify<br>- must have a Professional version of Visual Studio<br>- has moderate overhead, reducing polyphony a bit<br>- debug via a VST Client that you must also purchase<br>- a few DAWs do not support VST3 (yet)<br>- Visual Studio projects are complex; difficult to copy and rename a project<br>- no-built In Joystick programmer; you write the code for it |
| AU | - clean and relatively easy API<br>- uses XCode (free from Apple)<br>- runs with very little overhead for good polyphony count<br>- currently the de facto standard for Apple Logic software also supported in other clients like Ableton Live<br>- has similarities with iOS for iPhone/iPad development<br>- highly portable projects that do not require a specific folder hierarchy<br>- easy to copy and rename projects - only runs in MacOS<br>- is slightly different for OS 10.6 and earlier (this book only supports OS 10.7 and later the plug-ins are compatible)<br>- requires that your own GUI code in Objective-C (for native coding)<br>- flat Cocoa namespace requiring renaming of objects for each project<br>- build rules are quirky and require precise settings that are easy to forget/mess up<br>- no-built In Joystick programmer; you write the code for it |

In the sections that follow, many of the implementation details of the functions are here. The details as the book progresses and are fully explained on a chapter-by-chapter basis starting with Chapter 5, where you begin your first training-synth called NanoSynth. We will also go more in depth on making changes to the GUIs in later chapters.

As with any programming, you need to implement the projects before you really start to understand the API. This chapter will show you the underlying architecture and some of the code where future chapters will reveal the lower level details.

## 2.5 The RackAF Philosophy and API

The fundamental idea behind the RackAF soft is to provide a platform for rapidly developing real-time audio processing plug-ins with a minimum of coding, especially with regard to the User Interface. In fact, most of the details of the connection between the RackAFX plug-in and the RackAFX UI screen are hidden from the developer so that he may concentrate more on the audio signal.

The RackAFX API specifies the plug-in must be written in C++ and therefore takes advantage of the base class. The RackAFX plug-in will automatically create a derived class based on the project name. It will help you de-in focus on the UI.

You only need to implement the following functions:

- constructor()
- destructor()
- prepareForPlay()
- processAudio()
- userChange()
- midiNoteOn()
- midiNoteOff()
- midiPitchBend()
- midiModWheel()
- midiMessage()

## 2.6 Writing Plugins

Simply stated, RackAFX is the easiest way to write plug-ins. You use RackAFX to create the signal processing and not the UI. RackAFX also handles MIDI messages and is really MIDI-ready. It delivers MIDI messages to your plug-in and interfaces with your controllers: if you have a built-in piano-controller; however you need hardware MIDI controller to execute all the controller options like continuous and sustain pedal.

RackAFX sets up your compiler to develop your DLL in the /Plugins folder in the RackAFX Application Directory. If you want to see, move or delete a DLL, you can find this folder by using the menu item Plugin->Open Plugins or Menu->All Programs->RackAFX->Plugins.

Requirements:

- Windows OS (XP, Vista, 7, 8, 10)
- Visual Studio (Professional)
- http://www.pirkle.com/

# Creation

When you load a plug-in in RackAFX, you are actually setting the system path to the DLL you've created. RackAFX uses an OS function to load the DLL into its process space. Once the DLL is loaded, RackAFX first runs a compatibility test, then requests a pointer to the constructor called createObject(). It uses this pointer to call the method, and the DLL returns a newly created instance of your plug-in cast as the CPLugin base class type. From that point on, the RackAFX client can call any of the base class methods on your object. Figure 2.1 shows the flow of operation during the creation phase.
