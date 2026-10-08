```
if(! pRow->bEnable) continue;
```

```
// --- check the mod layer
if(!checkDestinationLayer(uModLayer, pRow)) continue;
```

```
// get the source value
double dSource = m_dSources[pRow->uSourceIndex];
```

```
switch(pRow->uSourceTransform) {
    case TRANSFORM_UNIPOLAR_TO_BIPOLAR:
        dSource = unipolarToBipolar(dSource);
        break;

case TRANSFORM_BIPOLAR_TO_UNIPOLAR:
        dSource = bipolarToUnipolar(dSource);
        break;

    <SNIP SNIP SNIP>
    default:
        break;
}
```

```
// destination += source*intensity*range
//
```

```
double dModValue = dSource*(pRow->pModIntensity)
    *(pRow->pModRange);
```

```
// first check DEST_ALL types
switch(pRow->uDestinationIndex);
```

polyphony. Figure 8.9 shows a simplified connection diagram for NanoSynth, and a conceptual diagram showing the single modulation matrix and each component owning a pointer to it.

The matrix is programmed in two steps; first, each object must be told where in the Sources or Destinations array