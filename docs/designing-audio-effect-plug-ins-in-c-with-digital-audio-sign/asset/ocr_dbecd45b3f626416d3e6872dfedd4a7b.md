![](bbox=[0.14, 0.0, 0.85, 0.16])

Figure 6.34: At the prescribed constant-Q value of Q = 1.414 we observe rippling and an increased high-frequency response with all controls at maximum boost.

![](bbox=[0.15, 0.25, 0.85, 0.33])

Figure 6.35: The cascaded graphic EQ topology; this is for a 10-band design using the exact unrounded ISO center frequencies. The design equations for each module use the constant-Q algorithm above.

![](bbox=[0.14, 0.42, 0.85, 0.59])

Figure 6.36: The 10-band constant-Q graphic EQ with the prescribed Q = 1.414 produces less low-frequency rippling and a decreased high-frequency response with all controls at maximum boost.

The constant-Q graphic EQ follows the same design pattern (Figure 6.35) except that you use the constant-Q peaking filter in each of the modules. The equations for finding the center frequencies and Q are the same as above. Bohn (1986) recommends not rounding the ISO center frequencies but rather use the exact values. Figure 6.36 shows the composite response with all controls set to full boost.

# 6.8 Design a Resonant LPF Plug-In

We'll continue with a resonant LPF design. The filter will use the second-order bilinear transform design and the bi-quad structure for implementation. After that you will redesign the filter using the Massberg technique for analog emulation and examine the differences. Note: This filter is found in RackAFX's module menu item under “HP/LP Filter” for you to experiment with and use to check your own implementations.

For this project, we'll be using our first built-in object. I've already prepared a bi-quad object for you