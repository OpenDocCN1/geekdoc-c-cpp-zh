
![](img/66c45bbed85bb7ba7f7b05dff49b5060_249_0.png)

**Figure 10.7.** The figure shows the effect of having different gamma functions for different channels. The green channel is kept the same in all the pictures (the red curve in the third row of Figure 10.6) while the red and blue channels are changed similarly for the left, middle and right picture respectively using respectively the red, green and blue curves in the third row of Figure 10.6. This results in different color tints in the different pictures – the right two are much warmer than the left one while the rightmost one is much more purplish than the other two.

for equal steps in input values. But, if we want to achieve a linear encoding on such displays, that provide uniform steps in output value for equal steps in input value, we would need a much larger number of bits – around 10-12 bits per pixel.

## 10.1.4 Example Displays

Displays are one of the most common devices where the effects of these different properties of color gamut, tone mapping operators and intensity resolution can be readily observed. So, let us study a few common display technologies from this perspective.

**Cathode Ray Tube (CRT) Displays:** CRT monitors excite phosphors with rays of electrons from an electron gun. Different types of phosphors are used to emit red, green and blue light. The phosphor colors match the sRGB color gamut, but they age easily becoming progressively less bright. In addition, the blue phosphor often degenerates faster leading to a change in color balance, giving the monitor a yellowish appearance. Note that though the hue and saturation of the primaries remain the same in the chromaticity diagram, the color of the display changes just due to deterioration of their brightness.

The CRT’s transfer function is a non-linear power function which is defined by the physics of the electron gun exciting the phosphors. In the simplest form, it is approximated as

```
$$I = V^{\gamma}$$
```

where $I$ is the measured intensity and $V$ is the input voltage corresponding to channel inputs. If the intensity produced at $V_0$ (black) is non-zero, then this equation is modified to

```
$$I = (V + V_0)^{\gamma}$$
```

Finally, the entire curve can be scaled by a constant $k$ to give the most general

form of the equation

I = k(V + V₀)^γ

The brightness and contrast controls in CRTs therefore change k and γ respectively.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_250_0.png)

Figure 10.8. The effects of flare light on the chromaticity of the primaries of an LCD display. The XYZ chromaticity coordinates of each channel are plotted (with red, green and blue color) as the input values are ramped from 0 to 1 while the other channels are left at zero. The black plots show the chromaticity coordinates of the grays as they ramp from 0 to 1. Left: With flare. Right: With flare subtracted. Note that with flare, each of these plots starts from the black offset chromaticity coordinates and move to the channel chromaticity value on a straight line as the input value increases thereby decreasing the effect of the black offset in the additive combination. If the black offset or flare is removed, the chromaticity coordinates are constant (since only the intensity changes with the change in input values).

### Liquid Crystal Displays (LCD):

LCD displays are a spatial array of red, green and blue segments, each of which is a colored filter over a cell of liquid crystal material that can be made variably transparent. A backlight shines through the LCD array so that the resulting color is a function of both the backlight and the filters. However, colored filters are significantly different than colored phosphors. The more intensely colored (saturated) the filter is, the less light it will pass making the display dim. The less saturated the filters, the brighter the display but it is also a lot less colorful. Thus, to get a highly bright and colorful display, very bright backlights are needed in addition to saturated color filters. But a trade-off needs to be made due to the huge power consumption. When compared to the gamut of the CRT displays, the blues of the LCD displays are often much less saturated.

The transfer function of LCDs is usually linear. But usually LCDs include electronics by which this can be changed to match the traditional CRT displays. Also, usually LCDs project some light even at input zero due to leaking of the backlight through the front of the display. Though it is called flare, it is the same as the black offset. Thus, the chromaticities of the primaries shift towards the white point for the lower intensities. Even with flare subtracted, the LCDs deviate measurably from the ideal RGB model since the chromaticity is still not constant at all brightness levels.

### Projection Displays:

A digital projector contains a digital imaging element like an LCD panel or an array of digital micromirrors (DMD) that modulate the light coming from a high intensity light bulb. Most LCD projectors and the larger DMD projectors have three imaging elements and a dichroic mirror that splits the white light from the bulb into its red, green and blue components. These are recombined and displayed through a single lens. The smaller projectors use a single imaging element with a wheel of filters, so that the separations are displayed sequentially in time. Some DLP (digital light processing) projectors have a fourth filter called the clear filter which are used while projecting the grays to achieve a higher brightness for grays. However, note that this is not equivalent to using more than three primaries since the chromaticity coordinate of the fourth filter lies inside the color gamut formed by the red, green and blue filters.

## 10.2 Color Management

So far we have been discussing a single device. Let us now consider multiple devices. When considering multiple devices, even if they are of the same type and same brand, the primaries in them can differ significantly. Especially, when we consider a complete imaging system including acquisition (using cameras), monitors, displays and printing, we need to make sure that the color in one device looks similar to that in another. You may have had the situation that your picture in the camera display looked nice and vibrant, but looked dull when projected in a slide projector for an event. Or, the printed picture looked washed out while the same picture looked perfectly fine in your monitor!

Color management entails modifying the input going to each device so that the output coming from each device matches. Since each device has different primaries, it is evident that they will need different inputs to create the same color. Since our goal is to maintain the same color across multiple devices, the only way to achieve this is to change the input from one device to another. We will consider two fundamental techniques of color management in this section.

### 10.2.1 Gamut Transformation

Let us consider two devices with linear gamma and color gamut defined by two different matrices $M_1$ and $M_2$. Let us assume that the input $(R_1,G_1,B_1)$ creates the color $(X,Y,Z)$ in the first device. Our goal is to find the input $(R_2,G_2,B_2)$ in the second device that would create the same color. Note that, as per Equation 10.10

$$\begin{pmatrix}X\\Y\\Z\end{pmatrix}=M_1\begin{pmatrix}R_1\\G_1\\B_1\end{pmatrix}=M_2\begin{pmatrix}R_2\\G_2\\B_2\end{pmatrix} \tag{10.18}$$

From the above equation, we find that

$$\begin{pmatrix}R_2\\G_2\\B_2\end{pmatrix}=M_2^{-1}M_1\begin{pmatrix}R_1\\G_1\\B_1\end{pmatrix} \tag{10.19}$$

Therefore, if we multiply the input to the first device with the matrix $M_2^{-1}M_1$, we will get the appropriate input to create the same color in the second device. This is called gamut transformation.

However, there are some issues with this technique as illustrated in Figure 10.9. Here we show the parallelepiped gamut of two devices, one in black and the other in gray. Let us now consider the color marked by the blue dot which is within the gamut of the first device. Once we apply our gamut transformation to find the corresponding input in the second device to produce the same color, the values we get are marked in the orange, magenta and cyan vectors. Note that the required color is outside the color gamut of the second device, and to reproduce that color one of the primaries has to be scaled by a value greater than 1.0. This means that the inputs generated will be out of the range. This indicates that the color to be generated is out of the device gamut and cannot be generated using convex combination of the primaries. Such colors are call out-of-gamut colors and cause a problem in any gamut transformation.

There are multiple ways to deal with out-of-gamut colors and they can be chosen based on the application. One option is to use an in-gamut color on the planar boundaries of the gamut that is closest to the out-of-gamut colors.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_252_0.png)

**Figure 10.9.** This figure illustrates the problem caused by out of gamut colors during gamut transformation.
