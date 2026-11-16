![](bbox=[0.18, 0.115, 0.71, 0.405])

Figure 6.1 (Blue) A graph of a signal with a perfect step edge. (Red) The same signal with Gaussian random noise added. (Green) The signal resulting from blurring with the kernel in Eq. 6.1.

The diffusion-based approach, e.g., Variable Conductance Diffusion (VCD), is compared with the MAP-based optimization method, and the two methods are shown to be equivalent. See section 6.6 for detail. The equivalence shows the relationship between energy minimization methods and spatial analysis methods and between their respective parameters of temperature and scale.

# ## 6.2 Image Smoothing

We begin by introducing a common concept, image smoothing. Initially, we discuss it in the context of a simple one-dimensional function.

# ### 6.2.1 The 1D Case

The noise in a one-dimensional discrete signal _f_(_x_) can be reduced simply by blurring the signal using a simple kernel like

```
1 2 4 2 1
```

which is a five-point approximated version of the one-dimensional Gaussian (recall section 5.4.4). In Figure 6.1, a step edge (recall section 5.5) with heights of zero and one has Gaussian random noise added, and then is blurred to remove the noise. Note that the blurred signal has reduced noise, but the edge is no longer sharp.