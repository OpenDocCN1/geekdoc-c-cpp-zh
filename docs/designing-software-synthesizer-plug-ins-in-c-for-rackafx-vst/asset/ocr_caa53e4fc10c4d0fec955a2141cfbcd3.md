# MIDI Functions

| MIDI Message | RackAFX | VST3 | AU |
|---|---|---|---|n| Pitch Bend | midiPitchBend() | process() | HandlePitchWheel() |
| Mod Wheel | midiModWheel() | process() | HandleControlChange() |
| All other MIDI Messages | midiMessage() | process() | HandleControlChange() HandleMidiEvent() |

Table 2.4: GUI functions for RackAFX, VST3 and AU.

| GUI Set and Maintenance |
| Detail | RackAFX | VST3 | AU |
|---|---|---|---|n| Declare/Describe Controls, set limits and defaults | done with an easy use Control Designer—you fill in a parameter that synthesizes the code for you | you must write the code yourself | you must write the code yourself |
| Initialize Controls | automatically written for you | you must write the code in initialize() | you must write the code in initialize() GetParameterInfo() GetParameterString() |
| Write control values to file (presets) | automatically written for you | you must write the code in getState() | automatically written for you |
| Read control values from file (presets) | automatically written for you | you must write the code in setState() | automatically written for you |
| Declare/Create GUI | automatically written for you | you must write the code in createView() | GUI Class Factory that you design and write |
| Graphical Design of GUI | Drag-And-Drop GUI built into RackAFX | Drag-And-Drop GUI via the VST3 Host | InterfaceBuilder in XCode |

Table 2.5: Comparison of the three platforms in this book.

| Platform | Pros | Cons |
|---|---|---|n| RackAFX | - simplest API with very few files and no GUI programming
- RackAFX writes some of the code for you
- supports multiple Visual Studio compilers including the free Expressions
- runs with very little system overhead for good polyphony count
- highly portable projects that do not require a specific folder hierarchy
- debug through RackAFX itself
- Vector Joystick programmer is built-in | - only runs in Windows
- for ported projects you must write and maintain your own GUI; can't drag-and-drop editor
- GUI controls are limited (fixed number of bitmap options, can not add your own graphics files)|