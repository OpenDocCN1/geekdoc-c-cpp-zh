need to do anything except call the base class implementation.

GetPresets()
is called at start-up time
and we fill in
an array of strings representing our presets names. The host then uses that array to populate its preset menu. The order of strings in the list must match your presets. In our case, we have only one preset so it is simple.

```
ComponentResult AUSynth::RestoreState(CFPropertyListRef plist)
    return AUInstrumentBase::RestoreState(plist);
```

```
OSStatus AUSynth::GetPresets(CArrayRef *outData) const {
    // --- this is used to determine if presets are supported
    // which in this unit they are so we implement this method!
    if (outData == NULL) return noErr;

    // --- make the array
    CFMutableArray theArray = CFArrayCreateMutable(NULL, numPresets, NULL);

    // copy our preset names
    for (int i = 0; i < numPresets; ++i) {
        CFArrayAppendValue(theArray, &presetNames[i]);
    }

    // --- set
    *outData = (CArrayRef)theArray;

    return noErr;
}
```

NewFactoryPreset() is called when the user loads a factory preset. We respond by updating our Global Parameters using the array of preset variables.