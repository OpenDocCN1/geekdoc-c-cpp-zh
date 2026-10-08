TRANSFORM_MIDI_NORMALIZE,
false); /* DISABLED BY DEFAULT */

m_GlobalModMatrix.addModMatrixRow(pRow);

# << INSERT ** Code Listing 8.7: Mod Matrix Routings III ** HERE >>

etc...

```
void Processor::update()
{
```

```
if(m_uNumberToDecayScaling == 1)
    m_GlobalModMatrix.enableModMatrixRow(SOURCE_MIDI_NOTE_NUM,
    DEST_ALL_EG_DECAY_SCALING,
    true);
else
    m_GlobalModMatrix.enableModMatrixRow(SOURCE_MIDI_NOTE_NUM,
    DEST_ALL_EG_DECAY_SCALING,
    false);
```

# << INSERT ** Code Listing 8.8: Mod Matrix Update II ** HERE >>

etc...

# StartNote() and StopNote()

Remove the old code and implement the functions using the code listings; the code is inserted after the MIDI logging statements and just before the end brackets.