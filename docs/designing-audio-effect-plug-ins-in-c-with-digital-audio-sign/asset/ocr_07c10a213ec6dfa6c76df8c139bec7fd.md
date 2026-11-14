GRL stands for gain reduction for the left and GRR stands for gain reduction for the right channel. Set up the two meters according to Table 13.2.

![](bbox=[0.305, 0.065, 0.695, 0.305])

# Figure 13.7: The 10 assignable meters in RackAFX.

# Table 13.2: Meter settings for the dynamics processor.

| Meter Blurb | GRL | Meter Blurb | Value |
|---|---|---|---|
| Invert Meter | true | Invert Meter | GRR |
| Enable Meter | true | Enable Meter | true |
| Meter Cal | linear | Meter Cal | linear |
| Detect Mode | PEAK | Detect Mode | PEAK |
| Meter Variable | m_fGRMeterValue_L | Meter Variable | m_fGRMeterValue_R |
| Attack Time | 0 | Attack Time | 0 |
| Release Time | 0 | Release Time | 0 |

The gain reduction value we will be metering is linear, from 0 to 1.0. The gain reduction value will have its own attack and release times according to our settings, so we want to monitor the PEAK variable type with no attack or release time.

All you need to do is make sure the variables m_fGRMeterValue_L and m_fGRMeterValue_R are reset to the current gain reduction value on each sample interval, and the meter will track it. The meter value needs to go up as the gain reduction goes down to visualize it properly. To set the meter, add one line of code to your processAudioFrame() function for each of the left and right channels.

# 13.1.5 DynamicsProcessor.cpp File

```
processAudioFrame()
```

+   • Add the metering variables to track the gain reduction values.