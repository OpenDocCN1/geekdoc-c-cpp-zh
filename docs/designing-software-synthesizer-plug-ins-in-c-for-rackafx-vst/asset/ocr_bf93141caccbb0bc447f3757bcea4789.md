```
// --- initialize the knobs
//
controlArray = [[NSMutableArray alloc] init];

// --- column
[wpRotaryKnob_0 initControlWithName:@"Noise Osc (dB)"
controlIndex:NOISE_OSC_AMP_DB
```

auval -v aumu MS03nWILL

If your validation does not succeed, go back and check your code. Once it succeeds, you are ready to debug the synth.

Debugging your synth-plugin is critical for your own code and the Chapter Challenges, As soon as you start experimenting with your own code, you will likely have problems as we do when implementing new code or ideas. To debug and test your plug-in, you will need an AU host (client); we have tested with AULab, Logic 9, Logic Pro X and Ableton 9. There are two ways to debug.

The easiest is to edit the Scheme for your project and choose an executable in the Run panel (described in the Appendix)—executable is the AU host. Then, you can set your breakpoints, to rebuild and launch the host for debugging in one step by clicking the triangular button. This method allows you to log strings to the console window.

You can also start the debugger after the client is running (you have to start the client manually). With the client running, Debug-Attach To Process and choose the client from the process list, then set breakpoints. When you instantiate your plug-in, the breakpoints will become active and you can step through the code and debug as usual. The difference is when you use the Attach To Process mechanism, you can't log information to the console window with printf statements. Debug logging is very useful, and we will use it in the next Chapter to log MIDI events. You will be flipping back and forth between your compiler and the plug-in client—this is normal for plug-in development on just any platform.

# Bibliography

Apple, Inc. "The Audio Unit Programming Guide." Accessed June 2014,
://developer.apple.com/library/mac/documentation/MusicAudio/Conceptual/AudioProgrammingGuide/Introduction.html

Pirkle, Will. 2012. Designing Audio Effects Plug-Ins in C++, Chap. 2. Burlington: Focal Press.

Rogerson, Dale. 1997. Inside COM, Chap. 1–7. Redmond: Microsoft Software.

Steinberg GmbH. "VST3 SDK." Accessed June 2014,
http://www.steinberg.net/en/cn/company/developers/sdk_download_portal.html