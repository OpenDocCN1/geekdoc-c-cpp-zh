![](bbox=[0.33, 0.0, 0.67, 0.105])

# Figure 12.4: The mod filter block diagram.

You used CBiquad in Chapter 6 to begin your filtering work. The CWaveTable object was taken directly from your WTOscillator object. You can find the definition and implementation in the pluginconstants.h and pluginobjs.cpp files. Table 12.1 shows the object's members and attributes. The flow chart for processAudioFrame() is shown in Figure 12.5.

# 12.1.1 Project: ModFilter

Create the project; because we are using built-in objects for the filter and LFO there are no member objects to add.

# 12.1.2 ModFilter GUI

For the initial design, you will need the following slider controls in Table 12.2. Note that these LFO waveform enumerations follow exactly that of the built-in CWaveTable object to make mapping the button control easy.

# 12.1.3 ModFilter.h File

Declare instances of the BiQuad and WaveTable objects. You don't need #include anything since these are built-in:

```
// Add your code here:-----------------------------------------------//
// BiQuad Objects
CBiquad m_LeftLPF;
CBiquad m_RightLPF;

// one LFO for the fc
CWaveTable m_fcLFO;
//-----------------------------------------------//
// END OF USER CODE
```

We are also going to need some variables and functions to control the effect. Specifically, we need:

+   • Minimum fc variable
+   • Maximum fc variable
+   • Function to calculate the current fc given a LFO value
+   • Functions to calculate the bi-quad coefficients for left and right channels independently (we want to calculate them separately for the third part of the project where we allow for quad-phase LFOs)

# Table 12.1: The CWaveTable object interface.