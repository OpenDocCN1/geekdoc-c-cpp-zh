# 44 CHAPTER 3 EXPRESSION BLEND

+   - Gradient Brush — The control is filled with a gradient brush that shades between colors. The following sections say more about gradient brushes.

+   - Tile Brush — The control is filled with a repeating image. The section “Tile Brushes” later in this chapter says more about tile brushes.

+   - Brush Resources — This tab lists predefined brush resources. They include system-brush colors such as ControlBrushKey and HighlightBrushKey, in addition to any brush resources that you have defined. The section “Tile Brushes” later in this chapter explains how to make some kind of brush resources.

Pick the brush you want, and then define the brush you want to use. The following sequences provide a little more detail about how to make some of the more complicated brushes.

# Gradient Brushes

A gradient brush fills an area with colors that flow smoothly from one to another. Depending on the type of brush, the colors can also include any number of colors, for example, it might shade from red to green to blue.

To create a brush, select the Brush area’s “Gradient brush” tab to select a Brush Editor similar to the one shown in Figure 3-7.

![](bbox=[0.678, 0.417, 0.868, 0.663])

Below the lists is a color square that you can click to select colors. Along the right edge of the square is a rainbow-like selector that you can click on to change the color square’s hue. In Figure 3-7, a pure green is selected so the color square shows different shades of green. If you clicked on the yellow part of the hue selector, the color square would display shades of yellow.

FIGURE 3-7

Beneath the color square is a horizontal bar showing the colors that make up your brush’s gradient. In Figure 3-7, the gradient starts green on the left, to dark green in the middle, and then shades back to light green on the right.

The little house-shaped tints below the gradient bar show key colors. If you click on one to select it, you can use other parts of the Brush Editor to change the color at that position. For example, you can click on the color square to pick the color’s value.

To the right of the color square and hue selector are R, G, and B textboxes where you can type color’s red, green, and blue components as values between 0 and 255.

The A textbox holds the color’s alpha component. (transparent) This value tells how opaque the color is and can take values between 0 percent (treshold) and 100 percent (opaque).

Below the A textbox is the color’s representation in hexadecimal.

Click-and-drag a key color to change its position in the gradient bar. Click on the color bar to add more key colors.

The final pieces of the Brush Editor described here let you decide whether the brush should be a linear gradient brush or a radial gradient brush. Click on the button in the Editor’s lower-left corner (it shades