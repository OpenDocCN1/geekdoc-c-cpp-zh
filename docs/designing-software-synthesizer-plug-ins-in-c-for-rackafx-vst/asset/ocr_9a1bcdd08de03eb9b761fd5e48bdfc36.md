DEST_ALL_FILTER_Q
DEST_ALL_EG_ATTACK_SCALING
DEST_ALL_EG_DECAY_SCALING

These make it easier to apply a single source to multiple destinations that all share the same intensity, range and transform attributes, which reduces the number of rows in the matrix.

The matlabRow structure has member variables for each of the items in Table 8.1. It is defined in synthfunctions.h as:

```
struct modMatrixRow {
    // --- index of source
    UINT uSourceIndex;

    // --- index of destination
    UINT uDestinationIndex;

    // --- needs to default to 1.0 in case no GUI control
    double* pModIntensity; // <- "ucControl" in MMA DLS
    double* pModRange; // <- "lScale" in MMA DLS

    // --- transform on Source
    UINT uSourceTransform;

    // --- to easily turn on/off a modulation routing
    bool bEnable;
}
```

This structure includes index values for a source and a destination. Notice that the intensity and range values are pointers; this is so you can control them directly from your plug-in's control variables. For example, when the user moves the EG1 to DCA Intensity control, they will be directly modifying this variable in the modulation matrix. A boolean variable enables or disables by row.

The transforms are indexed with another enumeration in synthfunctions.h. You can see thenTRANSFORM_NOTE_NUMBER_TO_FREQUENCY index, which we need for the Filter Key Track modulation. We will discuss the other transforms as we need, though their names are fairly self-explanatory.