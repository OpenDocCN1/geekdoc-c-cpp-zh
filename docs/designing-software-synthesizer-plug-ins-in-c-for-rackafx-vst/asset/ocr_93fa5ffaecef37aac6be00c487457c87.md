# Creating Rows

In the modulation matrix, you create all the rows dynamically at startup time; you add a row for every possible modulation supporting you even if some modulations are turned off by default. Another option is to create a matrix that can dynamically grow and shrink and remove rows on the fly. This opens up many potential traps and pitfalls, especially since both the processing and GUI threads need to access it. By creating a fixed matrix, we don't have those problems. You only need to set the bEnable flag for each row when you create the rows; default modulation rout are enabled while optional routings are disabled. In Section 8.11 we will experiment with turning rows on and off to let the user configure the patch from the GUI. Although you can create the rows yourself, we added a helper function in syncfunctions.h to create rows for you. This function is straightforward and self-explanatory.

```
enum transform {
TRANSFORM_NONE = 0,
TRANSFORM_UNIPOLAR_TO_BIPOLAR,
TRANSFORM_BIPOLAR_TO_UNIPOLAR,
TRANSFORM_MIDI_NORMALIZE,
TRANSFORM_INVERT_MIDI_NORMALIZE,
TRANSFORM_MIDI_TO_BIPOLAR,
TRANSFORM_MIDI_TO_PAN,
TRANSFORM_MIDI_TO_SWITCH,
TRANSFORM_MIDI_TO_ATTENUATION,
TRANSFORM_NOTE_NUMBER_TO_FREQUENCY,
MAX_TRANSFORMS
};
```

```
inline modMatrixRow* createModMatrixRow(UINT uSource
```

```
modMatrixRow* pRow = new modMatrixRow;
pRow->uSourceIndex = uSource;
pRow->uDestinationIndex = uDestination;
pRow->pIntensity = pIntensity;
pRow->pModRange = pRange;
pRow->uSourceTransform = uTransform;
pRow->bEnable = bEnable; // enable on/off

return pRow;
```