Build the plugin and load it into RackAFX, open the status window and play a few notes on your controller. You can see a few events logged at the top of the window—this is because RackAFX uses the status window to provide information to the user. You can tell the difference between message coming from a plug-in are indented. If you want to use the Status Window, get this first message logging properly, implement the rest of the MIDI logging.

# 3.6 NanoSynth: VST3

Use the TemplateSynth or TemplateSynth with MIDI project as a basis and follow the instructions in Appendix A to change it to NanoSynth. It comes pre-loaded with the header you need and your first file of a named VSynthParamLimits.h, which you will modify for every synth. If you want to practice by coding the MIDI logger in this chapter use the TemplateSynth; the other TemplateSynth with MIDI has the MIDI logging code for this chapter, but nothing else.

VST3 handles MIDI in an unusual and confusing manner. Right from the start, VST3 does not support the Voice Program Change (0xn where n = channel), so we will omit it from the VST3 versions of ours. The mechanism for handling Continuous Controller Messages is limited; in effort to make your life easier by mapping MIDI controllers directly to your controls, it is more difficult to create a modulation matrix where a controller may have multiple destinations and is to be configured on the fly. Some events such as note and off handled in a typical manner, but others are not. VST3 also offers its own kind of MIDI controller called Note Expression, though we will not use it in any of the book projects.

# 3.7 MIDI Events in VST3

VST3 breaks up the messaging into two parts: events and control changes. Events consist of note on, note off, polyphonic pressure (aftertouch), exclusive and two musical types: chord and scale. The different events are delivered as structures—different structure for each event. All chord and scale events contain the standard MIDI information of channel, note number, velocity, etc.

Events are packaged in the VST3 Event structure, which contains an event type index, and as a set of member structures packaged as a union. The event type index is named type. We will trap the following events type:

```
kNoteEvent
kNoteOffEvent
kPolyPressureEvent
```

Each type corresponds to one of the union's:

```
NoteOnEvent
noteOn
NoteOffEvent noteOff
PolyPressureEvent polyPressure
```

Placing the structs in a union makes it easy to access the various event attributes. The Event that is delivered to the doProcessEvent() is named vstEvent. For note on and note off, you retrieve the channel, note and velocity in ordinary MIDI range (0–127) like this:

note on:

```
UINT uMIDiChannel =
(UINT) vstEvent.noteOn.channel;
UINT uMIDINote =
(UINT) vstEvent.noteOn.pitch;
```