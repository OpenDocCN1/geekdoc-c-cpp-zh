colors. In RGB, [0,0,0] is black and [1,1,1] is white, whereas in CMY, [0,0,0] is white and [1,1,1] is black. Thus adding colors together in CMY makes them darker. This models the real-world observation that when two pigments (such as paint) are mixed together, the resulting substance subtracts out more of the surrounding light and becomes darker. That’s why the model is called subtractive: the values indicate the amount of light removed from surrounding light sources, even though we still combine colors by adding them together.

It is easy to convert back and forth between RGB and CMY by *inverting* the colors (subtracting them from [1,1,1] or white). One way of blending colors using CMY is to invert the RGB colors to generate CMY versions, add them, and then convert back to RGB:

color1_CMY = vec3(1,1,1) − color1_RGB
color2_CMY = vec3(1,1,1) − color2_RGB
blend_CMY = color1_CMY + color2_CMY
result_RGB = vec3(1,1,1) − blend_CMY

This works quite well if the colors of our panes are magenta (RGB=[1,0,1]), yellow (RGB=[1,1,0]), and cyan (RGB=[0,1,1]). Note that it is often necessary to scale the results down so that the final RGB color values don’t exceed 1.0. Figure 16.25 shows the resulting blends of colors produced by adding their CMY values.

![](bbox=[0.304, 0.569, 0.691, 0.886])

**Figure 16.25**
Adding cyan, magenta, and yellow panes in CMY color space.