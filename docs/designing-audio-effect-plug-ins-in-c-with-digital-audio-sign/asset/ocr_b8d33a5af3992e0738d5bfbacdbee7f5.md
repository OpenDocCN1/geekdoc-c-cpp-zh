short); you can have as many enumerated variables as you want, but in this case, we only need NORM and CROSS. Go to your plug-in's .h file to see the new variables:

![](bbox=[0.15, 0.07, 0.85, 0.47])

# Figure 7.32: The enumerated UINT data type.

```
// ADDED BY RACKAFX -- DO NOT EDIT THIS CODE!!!
// *** -0x07FD- ***

float m_FDelay_ms;
float m_Feedback_pct;
float m_FwetLevel_pct;
UINT m_uDelayType;
enum (NORM,CROSS);
// *** -0x1A7F- ***
```

For enumerated variables, the first one in the list will be the default, with the slider at the bottom. The other strings will appear in sequence when you move the slider up. The UINT will automatically be updated. We can use this as a directly controlled variable so there's nothing to add in userInterfaceChange(). Make the edits discussed next.

# 7.8.1 Constructor

+   • Initialize the delay type to NORM.