![](bbox=[0.35, 0.12, 0.8, 0.45])

Figure 7.6. Major eigenvector visualized with line glyphs colored by direction.

visualize the major eigenvector field using any of the vector visualization methods presented in Chapter 6. Figure 7.6 illustrates an application of this idea. Here, we show a hedgehog plot of the major eigenvector over a coronal slice in the same DT-MRI dataset used in Figure 7.3. Vectors are uniformly seeded at all points where the accuracy of the diffusion measurements are above a certain confidence level (similar to Figure 7.3). The hue of the vector coloring indicates their direction. For this, we use the following simple color-mapping function:

```
R = |e1 . x|,
G = |e1 . y|,
B = |e1 . z|.
```

Using this function, eigenvectors along the x-axis are colored in red, vectors along the y-axis are colored green, and vectors aligned with the z-axis of the dataset coordinate frame are colored blue, respectively. The icon in the bottom-right corner of Figure 7.6 illustrates the direction of color mapping. This icon has to be interpreted as a shaded sphere, where the color of each point maps the direction of the radial vector at that point. The luminance indicates the measurement confidence level. Bright vectors indicate high confidence measurement areas, whereas dark vectors indicate low confidence (noisy) measurements.