![](bbox=[0.35, 0.01, 0.65, 0.11])

Figure 12.2: An envelope generator can also modulate a filter parameter.

![](bbox=[0.32, 0.17, 0.68, 0.3])

Figure 12.3: A doubly modulated LPF with both $f_c$ and $Q$ controls.

# 12.1 Design a Mod Filter Plug-In: Part I Modulated $f_c$

For our first effect design, we'll start with a modulated second-order LPF and modulate the cutoff frequency with an LFO. Then, we can increase the complexity by adding another LFO to control the Q and even give the option to run the two LFOs in quadrature phase. We can use the second-order digital resonant LPF you've already designed from Chapter 6 for the filter. Notice that for this initial project, we will hold the LPF Q constant at 2.0. And, we will introduce a built-in RackAFX object to handle the LFO for us. The block diagram is shown in Figure 12.4.

The parameters are as follows:

+   - $f_c$ mod rate (0.2 to 10 Hz)
+   - $f_c$ mod depth (0 to 100%)
+   - LFO type (sine, tri, saw, square)
+   - LPF Q: fixed at 2.0
+   - $f_c$ mod range: 100 Hz to = kHz
+   - LPF is fixed as second-order bi-quad variety

By now, you should be getting really good at building RackAFX plug-ins. If you haven't just been cutting and pasting the code then you will have no problems with the next chapters. We can use the digital resonant LPF from Chapter 6 along with the built-in wave table oscillator object to quickly implement the mod filter effect. This project will use two built-in objects:

+   1. CBiquad for the filter
+   2. CWaveTable for the LFO