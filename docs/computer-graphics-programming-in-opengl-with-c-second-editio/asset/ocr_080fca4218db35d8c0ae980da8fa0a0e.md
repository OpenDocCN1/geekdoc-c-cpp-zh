Suppose that the darkened pixels are in shadow, as computed using shadow mapping. Instead of simply rendering the pixels as shown (i.e., with or without the diffuse and specular components included), suppose that we had access to neighboring pixel information, so that we could see how many of the neighboring pixels are in shadow. For example, consider the particular pixel highlighted in yellow in Figure 8.19, which according to Figure 8.18 is not in shadow.

![](bbox=[0.143, 0.256, 0.857, 0.403])

**Figure 8.19**  
PCF sampling for a particular pixel.

In the nine-pixel neighborhood of the highlighted pixel, three of the pixels are in shadow and six are not. Thus, the color of the rendered pixel could be computed as the sum of the ambient contribution at that pixel, plus six-ninths of the diffuse and specular contributions, resulting in a fairly (but not completely) brightened pixel. Repeating this process throughout the grid would produce pixel colors approximately as shown in Figure 8.20. Note that for those pixels whose neighborhoods are entirely in (or out of) shadow, the resulting color is the same as for standard shadow-mapping.

Unlike the example just shown, implementations of PCF do not sample every pixel within a certain vicinity of the pixel being rendered. There are two reasons for this: (a) we’d like to perform this computation in the fragment shader, but the fragment shader does not have access to other pixels; and (b) obtaining a sufficiently broad penumbra effect (say, ten to twenty pixels wide) would require sampling hundreds of nearby pixels for each pixel being rendered.

![](bbox=[0.143, 0.729, 0.33, 0.866])

**Figure 8.20**  
Soft shadow rendering.

PCF addresses these two issues as follows. First, rather than attempting to access nearby pixels, we instead sample nearby *texels* in the shadow map. The fragment shader can do this because even though it doesn’t have access to nearby pixel values, it does have access to the