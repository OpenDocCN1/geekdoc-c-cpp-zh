```
// --- set the AU Parameter; this calls SetParameter() in the au
AUParameterSet(AUEventListener, sender, &param,
    (Float32)floatValue, 0);

(IAction)WPOptionMenuItemChanged:(id)sender

if([sender respondsToSelector:@selector(controlID)] ||
    [sender respondsToSelector:@selector(getSelectedIndex)])
    return;

if([sender controlID] >= 0 {
    // -- get the OMG selection index
    Float32 floatValue = [sender getSelectedIndex];

    // -- make an AudioUnitParameter set in our AU buddy
    AudioUnitParameter param = (buddyAU, sender controlID,
        kAudioUnitScope_Global, 0);

    // -- set the AU Parameter; this calls SetParameter() in the au
    AUParameterSet(AUEventListener, sender, &param,
    (Float32)floatValue, 0);
}
```

initialize method is called using the method setKnobIndexArray.

Create each of the controls and add to the control.

The last part of the initializer finds, opens and stores the background image. For this synth, it is a brushed metal Bitmap. You can change the background image here, so free to experiment. The image will be tiled. The dealloc method releases the resources we've retained; notice that it also removes the Event Listeners we set up.

Lastly, the drawRect method tiles the background image and sets up the group frames for each row or column. The image for the frame is taken from the VSTGUI library and is stretched to fit. Simple graphics are calculated to place the row and column frames, and the drawRect is used to place the group image.

# 2.4 Implementing an AU Plug-in: Debugging

Before you load your plug-in into a client, it is vital that you validate it using Apple's AU validation tool. AU clients