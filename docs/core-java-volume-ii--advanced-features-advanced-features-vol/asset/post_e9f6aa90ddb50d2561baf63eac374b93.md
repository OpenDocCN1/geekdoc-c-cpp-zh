
### java.awt.Graphics2D 1.2

- `void clip(Shape s)` — intersects the current clipping shape with the shape s.
- `FontRenderContext getFontRenderContext()` — returns a font render context that is necessary for constructing TextLayout objects.

### java.awt.font.TextLayout 1.2

- `TextLayout(String s, Font f, FontRenderContext context)` — constructs a text layout object from a given string and font, using the font render context to obtain font properties for a particular device.
- `float getAdvance()` — returns the width of this text layout.
- `float getAscent()` / `float getDescent()` — returns the height of this text layout above and below the baseline.
- `float getLeading()` — returns the distance between successive lines in the font used by this text layout.

### 11.3.8 Transparency and Composition

In the standard RGB color model, every color is described by its red, green, and blue components. However, it is also convenient to describe areas of an image that are *transparent* or *partially transparent*. When you superimpose an image onto an existing drawing, the transparent pixels do not obscure the pixels under them at all, whereas partially transparent pixels are mixed with the pixels under them. Figure 11.51 shows the effect of overlaying a partially transparent rectangle on an image. You can still see the details of the image shine through from under the rectangle.

In the Java 2D API, transparency is described by an *alpha channel*. Each pixel has, in addition to its red, green, and blue color components, an alpha value between 0 (fully transparent) and 1 (fully opaque). For example, the rectangle in Figure 11.51 was filled with a pale yellow color with 50% transparency:

```java
new Color(0.7f, 0.7f, 0.0f, 0.5f);
```

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_758_0.png)

**Figure 11.51** Overlaying a partially transparent rectangle on an image

Now let us look at what happens if you superimpose two shapes. You need to blend or **compose** the colors and alpha values of the source and destination pixels. Porter and Duff, two researchers in the field of computer graphics, have formulated 12 possible *composition rules* for this blending process. The Java 2D API implements all of these rules. Before going any further, we'd like to point out that only two of these rules have practical significance. If you find the rules arcane or confusing, just use the `SRC_OVER` rule. It is the default rule for a `Graphics2D` object, and it gives the most intuitive results.

Here is the theory behind the rules. Suppose you have a *source* pixel with alpha value α_S. In the image, there is already a *destination* pixel with alpha value α_D. You want to compose the two. The diagram in Figure 11.52 shows how to design a composition rule.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_758_1.png)

**Figure 11.52** Designing a composition rule

Porter and Duff consider the alpha value as the probability that the pixel color should be used. From the perspective of the source, there is a probability α_S that it wants to use the source color and a probability of 1 − α_S that it doesn't care. The same holds for the destination. When composing the colors, let us assume that the probabilities are independent. Then there are four cases, as shown in Figure 11.52. If the source wants to use the source color and the destination doesn't care, then it seems reasonable to let the source have its way. That's why the upper right corner of the diagram is labeled 'S'. The probability for that event is α_S · (1 − α_D). Similarly, the lower left corner is labeled 'D'. What should one do if both destination and source would like to select their color? That's where the Porter–Duff rules come in. If we decide that the source is more important, we label the lower right corner with an 'S' as well. That rule is called SRC_OVER. In that rule, you combine the source colors with a weight of α_S and the destination colors with a weight of (1 − α_S) · α_D.

The visual effect is a blending of the source and destination, with preference given to the source. In particular, if α_S is 1, then the destination color is not taken into account at all. If α_S is 0, then the source pixel is completely transparent and the destination color is unchanged.

The other rules depend on what letters you put in the boxes of the probability diagram. Table 11.3 and Figure 11.53 show all rules that are supported by the Java 2D API. The images in the figure show the results of the rules when a rectangular source region with an alpha of 0.75 is combined with an elliptical destination region with an alpha of 1.0.

**Table 11.3 The Porter–Duff Composition Rules**

| Rule | Explanation |
|---|---|
| CLEAR | Source clears destination. |
| SRC | Source overwrites destination and empty pixels. |
| DST | Source does not affect destination. |
| SRC_OVER | Source blends with destination and overwrites empty pixels. |
| DST_OVER | Source does not affect destination and overwrites empty pixels. |
| SRC_IN | Source overwrites destination. |
| SRC_OUT | Source clears destination and overwrites empty pixels. |
| DST_IN | Source alpha modifies destination. |
| DST_OUT | Source alpha complement modifies destination. |
| SRC_ATOP | Source blends with destination. |
| DST_ATOP | Source alpha modifies destination. Source overwrites empty pixels. |
| XOR | Source alpha complement modifies destination. Source overwrites empty pixels. |

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_760_0.png)

**Figure 11.53** Porter–Duff composition rules

As you can see, most of the rules aren't very useful. Consider, as an extreme case, the `DST_IN` rule. It doesn't take the source color into account at all, but uses the alpha of the source to affect the destination. The `SRC` rule is potentially useful—it forces the source color to be used, turning off blending with the destination.

For more information on the Porter–Duff rules, see, for example, *Computer Graphics: Principles and Practice, Second Edition in C*, by James D. Foley, Andries van Dam, Steven K. Feiner, et al.

Use the `setComposite` method of the `Graphics2D` class to install an object of a class that implements the `Composite` interface. The Java 2D API supplies one such class, `AlphaComposite`, that implements all the Porter–Duff rules in Figure 11.53.

The factory method `getInstance` of the `AlphaComposite` class yields an `AlphaComposite` object. You supply the rule and the alpha value to be used for source pixels. For example, consider the following code:

```java
int rule = AlphaComposite.SRC_OVER;
float alpha = 0.5f;
g2.setComposite(AlphaComposite.getInstance(rule, alpha));
g2.setPaint(Color.blue);
g2.fill(rectangle);
```

The rectangle is then painted with blue color and an alpha value of 0.5. Since the composition rule is `SRC_OVER`, it is transparently overlaid on the existing image.

The program in Listing 11.17 lets you explore these composition rules. Pick a rule from the combo box and use the slider to set the alpha value of the `AlphaComposite` object.

Furthermore, the program displays a verbal description of each rule. Note that the descriptions are computed from the composition rule diagrams. For example, a “DS” in the second row stands for “blends with destination.”

The program has one important twist. There is no guarantee that the graphics context that corresponds to the screen has an alpha channel. (In fact, it generally does not.) When pixels are deposited to a destination without an alpha channel, the pixel colors are multiplied with the alpha value and the alpha value is discarded. Now, several of the Porter–Duff rules use the alpha values of the destination, which means a destination alpha channel is important. For that reason, we use a buffered image with the ARGB color model to compose the shapes. After the images have been composed, we draw the resulting image to the screen.

```java
var image = new BufferedImage(getWidth(), getHeight(), BufferedImage.TYPE_INT_ARGB);
Graphics2D gImage = image.createGraphics();
// now draw to image
g2.drawImage(image, null, 0, 0);
```

Listings 11.17 and 11.18 show the frame and component class. The Rule class in Listing 11.19 provides a brief explanation for each rule—see Figure 11.54. As you run the program, move the alpha slider from left to right to see the effect on the composed shapes. In particular, note that the only difference between the `DST_IN` and `DST_OUT` rules is how the destination (!) color changes when you change the source alpha.
