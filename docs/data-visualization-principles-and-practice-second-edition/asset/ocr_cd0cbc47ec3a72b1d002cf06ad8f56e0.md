![](bbox=[0.08, 0.12, 0.75, 0.35])

Figure 5.3. Visualizing the scalar function \( e^{-10(x^2+y^4)} \) with (a) a luminance colormap and (b) a zebra colormap. The luminance colormap shows absolute values, whereas the zebra colormap emphasizes rapid value variations.

which are the regions where the data has similar rates of variation across our domain.

Interpolation issues. Another important aspect of color mapping is the relationship between the colormap design, scalar data variation speed, and domain sampling frequency.

Figure 5.5 illustrates this by means of an example—a sphere geometry on which a periodic sine function is visualized with a rainbow colormap. The mesh is overlaid on top of the visualization to emphasize the sampling frequency. The periodic band structure of the function is clearly visible in Figure 5.4(a), where the sphere is sampled at a \( 64 \times 64 \) resolution. However, the structure starts getting noisy as we decrease the sampling resolution (Figure 5.4(b), \( 32 \times 32 \) samples). If the resolution is decreased further, we obtain a completely incorrect visualization (Figure 5.4(c)) that suggests a completely different function than the actual one to the unprepared user.

To explain the problem, consider the color-mapping implementation: First, color mapping (Equation 5.1) is applied at the grid vertices \( p_i \) yielding one color attribute \( c(s_i) \) per vertex. Here, \( s_i \) denotes the scalar attribute value stored at vertex \( p_i \). Next, the surface cells are rendered as colored polygons, using the color interpolation provided by the polygon rendering machinery. Hence, the