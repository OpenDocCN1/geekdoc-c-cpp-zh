# 6.8.2 ResonantLPF GUI

Figure 6.37 shows what your final GUI will look like. You will need the controls shown in Table 6.3.

![](bbox=[0.4, 0.08, 0.6, 0.22])

# Figure 6.37: The resonant LPF GUI.

# Table 6.3: The GUI controls for the resonant LPF.

| Slider Property | Value |
|---|---|
| Control Name | Fc |
| Units | Hz |
| Variable Type | float |
| Variable Name | m_f_fc_Hz |
| Low Limit | 100 |
| High Limit | 5000 |
| Initial Value | 1000 |

| Slider Property | Value |
|---|---|
| Control Name | Q |
| Units | |
| Variable Type | float |
| Variable Name | m_f_Q |
| Low Limit | 0.5 |
| High Limit | 20 |
| Initial Value | 0.707 |

# 6.8.3 ResonantLPFh File

RackAFX provides you with the built-in bi-quad object named CBiquad and you don't need to do anything at all to add it to your project. You can just declare your bi-quad objects directly in the .h file like you would any other object:

```
CBiquad m_LeftLPF; // or whatever you like to name it
```