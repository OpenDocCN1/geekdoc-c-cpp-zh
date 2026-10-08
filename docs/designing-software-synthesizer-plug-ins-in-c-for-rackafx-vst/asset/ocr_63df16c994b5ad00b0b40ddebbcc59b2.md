# CModulationMatrix Member Variables

| Type | Variable Name | Description |
|---|---|---|n| modMatrixRow** | m_ppMatrixCore | pointer to array of matrix row pointers–the core |
| int | m_nSize | number of-NULL rows in core |
| double [] | m_dSources | array of source registers |
| double [] | m_dDestinations | array of destination registers |

# CModulationMatrix Member Functions

| Function Name | Description |
|---|---|
| getMatrixCore | returns the pointer to the matrix core |
| setMatrixCore | sets the matrix core pointer |
| getMatrixSize | returns the number of-NULL rows |
| clearMatrix | clears core matrix, does not delete pointers |
| clearSources | clears source array |
| clearDestinations | clears destination array |
| addMatrixRow | adds a new row, checks to see if row exists before adding |
| matrixRowExists | checks to see if a row exists |
| createMatrixCore | creates a new matrix; deletes existing core |
| deleteMatrix | deletes rows then deletes matrix array |
| enableDestinationRow | enables or disables an existing row for flexible routing |
| checkDestinationLayer | checks to see if a destination is in a layer N group |
| doModulationMatrix | do the matrix operation |

```
// --- current size depending on number of rows added
int m_nSize;
```

public:

```
// sources: where each source (LFO, EG, ETC) writes its output value
double m_dSources[MAX_SOURCES];
```

```
// destinations: where the newly calculated mod values are read from
double m_dDestinations[MAX_DESTINATIONS];
```

# getModMatrixCore() and setMatrixCore()

The getModMatrixCore() and setMatrixCore() simply get and set the pointer; during the set, the matrix is deleted if it already exists. The matrix core is dynamically allocated during construction. getMatrixSize() just iterates through the rows and calculates the size.