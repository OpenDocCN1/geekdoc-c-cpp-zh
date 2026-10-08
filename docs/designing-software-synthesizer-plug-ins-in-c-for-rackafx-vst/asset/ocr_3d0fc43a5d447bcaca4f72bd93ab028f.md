The synthesizer's polyphony is maintained by maintaining an array of voice pointer objects. This array is named m_pVoiceArray for all the synths. The difference is in the kind of pointers they hold; in this case the array holds Synth pointers. The three functions below its definition are for handling the time ordering of the voices. The update() function is for updating all the synth variables at once. We will get into the details of these as well as the few remaining variables as Chapters 3–12 progress.

Now, let's look at each function implementation by one. The synth projects are all very similar from the plug-in object's point of view. Most of the work that differentiates the synths is done in the CVoice objects that we will design. So, once you understand one synth, the others are very easy to grasp. Open the MiniSynth.cpp file, and let's start at the top and work our down through the implementation.

# constructor

The constructor in each RackAFX plug-in does the following:

+   - initUI() on the very first line to instantiate and initialize your GUI control objects
- initialize derived class variables
- set m_bWantAllMIDIMessages = true so we can get all MIDI messages
- initialize our custom variables
- create the voice objects and load them into the array

Much of the constructor was written for you when you created the project; these variables do not need to be altered, so you can safely ignore them here. Perhaps the most important part is at the end where the voices are allocated.