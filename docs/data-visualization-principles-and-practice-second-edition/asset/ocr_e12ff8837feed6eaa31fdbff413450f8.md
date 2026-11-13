![](bbox=[0.095, 0.12, 0.745, 0.33])

(a) c1 linear estimator   (b) fractional anisotropy   (c) relative anisotropy

Figure 7.5. Different anisotropy measures for diffusion tensor data.

tional anisotropy for the same dataset and slice as for the c1 certainty discussed before. Again, the corpus callosum area is clearly viewable in this image.

A related measure is the relative anisotropy [Pierpaoli and Basser 96], defined as

```
RA = \sqrt{\frac{3}{2}} \frac{\sqrt{\sum_{i=1}^3 (\lambda_i - \mu)^2}}{\lambda_1 + \lambda_2 + \lambda_3}. \quad (7.12)
```

Figure 7.5(c) shows the relative anisotropy for the previous dataset.

Overall, the methods presented in this section reduce the visualization of a tensor field to that of one or more scalar quantities, such as the anisotropy, computed from the PCA analysis performed on the tensor data. These can be examined using any of the scalar visualization methods presented in Chapter 5, such as color plots, slice planes, and isosurfaces.

# 7.4 Visualizing Vector PCA Information

In the previous section, we saw how to visualize various anisotropy metrics computed from the PCA analysis of a tensor field using standard scalar visualization methods such as color mapping. However, in many cases, we are interested in visualizing not just the amount of anisotropy, but also the directions in which this anisotropy takes place.

Let us start with the simpler case when we are interested only in the direction of maximal variation of our tensor-encoded quantity. For this, we can