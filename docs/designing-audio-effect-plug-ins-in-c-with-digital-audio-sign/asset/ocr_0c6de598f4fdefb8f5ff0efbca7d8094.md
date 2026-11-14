+   • DDLModule.h (because ModDelayModule # includes it).
+   • WTOscillator.h (because DDLModule #includes it).

# ## 10.4.2 StereoQuadFlanger GUI

We will use a simpler UI consisting of the controls shown in Table 10.4.

# ## 10.4.3 StereoQuadFlanger.h File

In the .h file, declare two instances of the ModDelayModule, one for the left and one for the right. Also add one helper function to initialize and update the modules. These two member variables and the one function are all that you need.

```
// Add your code here:
//-------------------------------------------------------------- //
CModDelayModule m_ModDelayLeft;
CModDelayModule m_ModDelayRight;

void updateModDelays();
//-------------------------------------------------------------- //
// END OF USER CODE
```

Table 10.4: The GUI elements for the StereoQuadFlanger.

| Slider Property | Value |
|---|---|
| Control Name | Depth |
| Units | % |
| Variable Type | float |
| Variable Name | m-fModDepth-pct |
| Low Limit | 0 |
| High Limit | 100 |
| Initial Value | 50 |

| Slider Property | Value |
|---|---|
| Control Name | Feedback |
| Units | % |
| Variable Type | float |
| Variable Name | m-fFeedback-pct |
| Low Limit | -100 |
| High Limit | 100 |
| Initial Value | 50 |

| Slider Property | Value |
|---|---|
| Control Name | Rate |
| Units | Hz |