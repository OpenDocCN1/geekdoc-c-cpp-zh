
portion. This is called a *subtractive* color effect, and is how colors blend when, for example, mixing paint or ink.

However, suppose that these panes were actually *emitting* colors, rather than filtering them — such as if a yellow light source was combined (*added*) to a blue light source. In that case, the yellow and blue panes would *not* combine to form green. Thus, depending on what we wish to model, we need to blend colors in different ways.

So far, all of our colors have been expressed using the RGB color model. RGB is an example of an *additive* color model, and it is designed for *blending light sources* — most specifically the red, green, and blue elements of an RGB computer monitor — by adding them together. That is, it is designed not to “mix” its colors like paint, but ideally to *add* them. When mixing paint, we expect each successive combined color to *darken* the mix (because each successive color subtracts some portion of the light). However, in an additive model which blends light sources, each successive color *brightens* the mix, moving it closer and closer to white light.

Another thing about the RGB model that is a common source of confusion is that it is designed with primary colors red, green, and blue, rather than the familiar red, *yellow*, and blue primary colors for paints or crayons that most of us learned in elementary school. The RGB primary colors work very well if our three panes are light sources. Suppose for example that we replaced the red/yellow/blue panes with red/green/blue panes, and simply *added* their colors, without weights, as in the following:

mixed_color = pane_color + refracted_color;

The result is shown in Figure 16.24.

![](img/1695de1bc7486362f86c143285f3fb40_470_0.png)

**Figure 16.24**  
A scene with three overlapping colored light sources, colors added together

To most people new to color models, Figure 16.24 looks very strange (it looks even stranger with red/yellow/blue panes – try it!). The red and blue panes combine to form a sort of light purple called *magenta*, which probably seems fairly reasonable – but few people expect red and green would combine to make yellow. And yet, if these panes were *light sources*, believe it or not, this is much closer to what would actually happen in the real world. Note, for example, that at the very center, all three red/green/blue primary light colors have been added together, resulting in full spectrum white light. So the RGB additive color model, when used to blend colors by adding them, is accurate when we use it to blend colored light sources.

But what if we want to model colored objects that aren’t light sources, but are instead passive colored objects responding to white light sources, such as a colored window pane or a pair of orange sunglasses? It turns out that the additive RGB model is quite clumsy for this task.

If colored transparent objects are desired, rather than light sources, one option is to switch to a *subtractive* color model, such as CMY (cyan/magenta/yellow). Whereas RGB is designed for computer monitors composed of tiny red, blue, and green light emitters, CMY is commonly used for printers that mix ink to build colors. In RGB, [0,0,0] is black and [1,1,1] is white, whereas in CMY, [0,0,0] is white and [1,1,1] is black. Thus adding colors together in CMY makes them darker. This models the real-world observation that when two pigments (such as paint) are mixed together, the resulting substance subtracts out more of the surrounding light and becomes darker. That’s why the model is called subtractive: the values indicate the amount of light removed from surrounding light sources, even though we still combine colors by adding them together.

It is easy to convert back and forth between RGB and CMY by *inverting* the colors (subtracting them from [1,1,1] or white). One way of blending colors using CMY is to invert the RGB colors to generate CMY versions, add them, and then convert back to RGB:

$$\begin{aligned}
color1_{CMY} &= vec3(1,1,1) - color1_{RGB} \\
color2_{CMY} &= vec3(1,1,1) - color2_{RGB} \\
blend_{CMY} &= color1_{CMY} + color2_{CMY} \\
result_{RGB} &= vec3(1,1,1) - blend_{CMY}
\end{aligned}$$

This works quite well if the colors of our panes are magenta (RGB=[1,0,1]), yellow (RGB=[1,1,0]), and cyan (RGB=[0,1,1]). Note that it is often necessary to scale the results down so that the final RGB color values don’t exceed 1.0. Figure 16.25 shows the resulting blends of colors produced by adding their CMY values.

![](img/1695de1bc7486362f86c143285f3fb40_472_0.png)

**Figure 16.25**  
Adding cyan, magenta, and yellow panes in CMY color space

It turns out that the results are rather similar if we start with these same magenta, yellow, and cyan panes, and blend their RGBs with a weighted sum as we have been doing earlier in this chapter, as shown in Figure 16.26.

![](img/1695de1bc7486362f86c143285f3fb40_472_1.png)

**Figure 16.26**  
Blending cyan, magenta, and yellow panes in RGB color space

To summarize, we have learned thus far that blending RGB colors for light *sources* works very well by simply adding the RGB colors, but blending RGB colors for transparent panes (as if we are mixing paint) is more problematic. Depending on the colors being used, some applications may suffice by using one of the two methods just described, that is, either converting the colors to CMY, adding them, and converting back to RGB, or simply blending the two colors in RGB with a weighted sum. Figure 16.27 shows both methods in three scenarios: red/yellow/blue, red/green/blue, and magenta/yellow/cyan panes.

![](img/1695de1bc7486362f86c143285f3fb40_473_0.png)

**Figure 16.27**  
Adding in CMY color space (top row) and blending in RGB color space (bottom row).

In each of the methods shown in Figure 16.27, there is at least one color combination that would appear incorrect for mixing paint (or stacking glass panes). Therefore, if an application requires correct subtractive blending across the color spectrum, none of the above methods will be adequate, and another method is needed.

A third approach for handling colored panes is to convert the colors from an RGB color model to an RYB subtractive model based on primary colors red/yellow/blue. Precise algorithms for doing this tend to be complex. Sugita and Takahashi [ST15] described a surprisingly simple algorithm for converting between RGB and RYB that isn’t perfect but works pretty well across the color spectrum. Program 16.16 shows GLSL implementations of their conversion functions, which may be practical for many cases.

## Program 16.16 – Blending via Conversion to RYB

### Compute Shader

```glsl
...
void process_stack_element(int index)
{
    // during phase 4 blending:
    if ((objects[index].object_index).isTransparent)
    {
        vec3 mixedRYB = rgb2ryb(mixed_color);
        vec3 refractedRYB = rgb2ryb(refracted_color);
        mixed_color = ryb2rgb(mixedRYB + refractedRYB);
    }
    ...
}

vec3 rgb2ryb(vec3 rgb)
{
    float white = min(rgb.r, min(rgb.g, rgb.b)); // compute white and black contributions for input color
    float black = min((1-rgb.r), min((1-rgb.g), (1-rgb.b))); // assumes colors are clamped to the range [0, 1]
    vec3 rgbWhiteRemoved = rgb - white; // remove white from input color before converting to RYB

    // build initial RYB values for the output color
    vec3 buildRYB = vec3(
        rgbWhiteRemoved.r - min(rgbWhiteRemoved.r, rgbWhiteRemoved.g),
        (rgbWhiteRemoved.g + min(rgbWhiteRemoved.r, rgbWhiteRemoved.g)) / 2.0,
        (rgbWhiteRemoved.b + rgbWhiteRemoved.g - min(rgbWhiteRemoved.r,
            rgbWhiteRemoved.g)) / 2.0);

    float normalizeFactor = max(buildRYB.x, max(buildRYB.y, buildRYB.z))
        / max(rgbWhiteRemoved.r, max(rgbWhiteRemoved.g, rgbWhiteRemoved.b));
    buildRYB /= normalizeFactor;          // normalize for similar white level
    buildRYB += black;                    // normalize for similar black level
    return buildRYB;
}
```
