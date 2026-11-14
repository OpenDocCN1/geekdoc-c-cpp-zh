data type, using either a slider or radio-button bank. I will use another radio button bank in this example.

# # 9.7.1 WTOscillator GUI

Start with the UI and add another enumerated UINT by right-clicking inside the second bank of radio buttons and filling out the properties in Table 9.4.

# Table 9.4: The button properties for the mode switches between “normal” and “bandlimited” on the UI.

| Slider Property | Value |
| :--- | :--- |
| Control Name | Osc Type |
| Units | |
| Variable Type | enum |
| Variable Name | m_uOscType |
| enum string | normal, bandlimit |

# # 9.7.2 WTOscillator.h File

This new information appears in the .h file:

```
// ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!! -------------------------------------- //
/**--0x07FD--**/
float m_fFrequency_Hz;
UINT m_uOscType;
enum{sine,saw,tri,square};
UINT m_uTableMode;
enum{normal, bandlimit};
/**--0x1A7F--**/
// ------------------------------------------------------------- //
```

As long as we are in the .h file, we need to add more arrays for our band-limited tables. We want to keep these separate from the other tables to provide both modes of operation.