```
char* pPath0 = addStrings(componentFolder,"/MultiSamples/Heaver");
char* pPath1 = addStrings(componentFolder,"/MultiSamples/OldFlatty");
char* pPath2 = addStrings(componentFolder,"/MultiSamples/Divider");
char* pPath3 = addStrings(componentFolder,"/MultiSamples/FuzzVibe");
//
```

```
// to speed up sample loading, init the first voice we
init(false, false) = NOT single-sample, NOT pitchless sample
if(im_pVoiceArray[0]->initOscWithFolderPath(0, pPath0, false, false))
    return false;
if(im_pVoiceArray[0]->initOscWithFolderPath(1, pPath1, false, false))
    return false;
if(im_pVoiceArray[0]->initOscWithFolderPath(2, pPath2, false, false))
    return false;
if(im_pVoiceArray[0]->initOscWithFolderPath(3, pPath3, false, false))
    return false;
// then use the other function to copy the sample pointers
// so share pointers to same buffers of data
for(int i=1; i<MAX_VOICES; i++)
```

DigiSynth to match the new variable additions/removals listed above. In the switch/case statement, delete the case statements for the removed variables and add case statements for the new ones, shown here in bold. These are the same additions/removals you implemented in the update() function. Notice also that you pick up the vector joystick position here; it comes from the new joystick control.

# 11.16 VectorSynth: AU

Create a new project VectorSynth and set the GUI using Table 11.6. Add the new vector joystick control as described in Section 11.9.

# AUSynth.h

At the top of the file, add the #include statement for VectorVoice.h and set up the array of voices and all helper member functions. Add the loadSamples() function as well.

# AUSynth.cpp

The following functions are identical to DigiSynth, with the exception of the type of voice pointers created and stored in the array.

+   - destructor