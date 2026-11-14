implement the linear interpolation but the easiest method is to treat it like a DSP filter. Another way of thinking about interpolation is as a weighted sum. For example, if the interpolation point is 0.5 between samples 1 and 2, then the interpolated value is made up of 50% of sample 1 plus 50% of sample 2. In the above case, our interpolated distance is 0.7183, so we can view the output as

![](bbox=[0.18, 0.11, 0.82, 0.32])

# Figure 7.26: Linear interpolation of sample values.

![](bbox=[0.32, 0.38, 0.68, 0.55])

# Figure 7.27: Linear interpolation as a kind of feed-forward filter. The z⁻¹ element is removed since we do not know if the interpolated samples will always be exactly one sample apart. For example, what if the next fractional delay sample is at location 56.2394?

```
interp_output = (0.7183)(Sample 2) + (0.2817)(Sample 1)
```

Here is a linear interpolation function you can use; it is already declared in your pluginconstants.h file:

```
float dLinTerp (float x1, float x2, float y1, float y2, float x);
```

You give it a pair of data points (x1,y1) and (x2,y2), plus a distance between them on the x-axis (x), and it returns the interpolated value using the weighted sum method. The first part of the code checks for a potential divide by zero fault that technically should not happen. You should also be aware that linear interpolation is a form of feed-forward filtering. The block diagram of the above function would look like Figure 7.27.

Thus, in the processAudioFrame(), we need to find the two sample values that our actual delay time needs, then do the interpolation. It is pretty straightforward except the situation where we are interpolating across the wrap boundary (from the last sample in the buffer to the first one). Suppose the user enters a delay time that corresponds to 2.4 samples of delay. In the cookVariables() function,