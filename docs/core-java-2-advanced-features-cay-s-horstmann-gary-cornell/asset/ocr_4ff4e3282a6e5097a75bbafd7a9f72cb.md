# Table 11.2 *(Continued)*

| Key | Value | Explanation |
|---|---|---|
| KEY_RENDERING | VALUE_RENDER_QUALITY<br>VALUE_RENDER_SPEED<br>VALUE_RENDER_DEFAULT | When available, select the rendering algorithm for greater quality or speed. |
| KEY_STROKE_CONTROL 1.3 | VALUE_STROKE_NORMALIZE<br>VALUE_STROKE_PURE<br>VALUE_STROKE_DEFAULT | Select whether the placement of strokes is controlled by the graphics accelerator (which may move it by up to half a pixel) or is computed by the “pure” rule that mandates that strokes run through the centers of pixels. |
| KEY_DITHERING | VALUE_DITHER_ENABLE<br>VALUE_DITHER_DISABLE<br>VALUE_DITHER_DEFAULT | Turn dithering for colors on or off. Dithering approximates color values by drawing groups of pixels of similar colors. (Note that antialiasing can interfere with dithering.) |
| KEY_ALPHA_INTERPOLATION | VALUE_ALPHA_INTERPOLATION_QUALITY<br>VALUE_ALPHA_INTERPOLATION_SPEED<br>VALUE_ALPHA_INTERPOLATION_DEFAULT | Turn precise computation of alpha composites on or off. |
| KEY_COLOR_RENDERING | VALUE_COLOR_RENDER_QUALITY<br>VALUE_COLOR_RENDER_SPEED<br>VALUE_COLOR_RENDER_DEFAULT | Select quality or speed for color rendering. This is only an issue when you use different color spaces. |
| KEY_INTERPOLATION | VALUE_INTERPOLATION_NEAREST_NEIGHBOR<br>VALUE_INTERPOLATION_BILINEAR<br>VALUE_INTERPOLATION_BICUBIC | Select a rule for interpolating pixels when scaling or rotating images. |

The most useful of these settings involves antialiasing. This technique removes the “jaggies” from slanted lines and curves. As you can see in Figure 11.25, a slanted line must be drawn as a “staircase” of pixels. Especially on low-resolution screens, this line can look ugly. But if, instead of drawing each pixel completely on or off, you color in the pixels that are partially covered with the color value proportional to the area of the pixel that the line covers, then the result looks much smoother. This technique is called antialiasing. Of course, antialiasing takes a bit longer because it has to compute all those color values.