```
void c(float f ,float& R,float& G,float& B)
{
    const float dx = 0.8;
    f = (f<0) ? 0 : (f>1) ? 1 : f;        //clamp f in [0,1]
    g = (6-2*dx)*f + dx;                  //scale f to [dx, 6 - dx]
    R = max(0,(3 - fabs (g-4) - fabs (g -5))/2);
    G = max(0,(4 - fabs (g-2) - fabs (g -4))/2);
    B = max(0,(3 - fabs (g-1) - fabs (g -2))/2);
}
```

# Listing 5.1. Rainbow colormap construction.

Rainbow colormaps are one of the widest used colormap types in data visualization, and they are included, and often provided as default, in numerous visualization applications [Borland and Taylor 07]. However, the rainbow colormap has also several important limitations:

+   Focus: Perceptually, warm colors arguably attract attention more than cold colors. In our example in Figure 5.2(a), this means our attention is attracted more towards the high data values. This can be desirable if these are our values of interest (goal 4). However, depending on the application, these may not be the values where we want to focus on.

+   Luminance: The construction of the rainbow colormap proposed in Figure 5.1 and Listing 5.1 states that all generated colors have the same HSV luminance, i.e., the same maximum of the R, G, and B color components (see Section 3.6.3, Listing 3.2), except for the “tails” of the colormap, where the luminance is slightly increasing, respectively slightly decreasing. However, as explained by Section 3.6.3, Equation 3.23, perceived luminance and HSV luminance are far from being identical. As such, luminances of the rainbow colormap entries vary non-monotonically. This leads to users being potentially attracted more to certain colors than to others, and/or perceiving certain color contrasts as being more important than others. The latter issue can create problems for goal 5. This issue can be corrected by adjusting the rainbow colormap entries so that they use the same hues, but have maximal luminance as being given by Equation 3.23.

+   Context: Hues can have application-dependent semantics. The rainbow colormap is based on the assumption that “warm” colors, such as yellow and red, are perceived as being associated with higher data values, whereas “cold” colors such as blue suggest low values. This assumption is based on the interpretation of the rainbow colormap as a heat, or temperature,