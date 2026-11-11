![](bbox=[0.324, 0.141, 0.764, 0.271])

**Figure 11.21** Overlaying a partially transparent rectangle on an image

Now let us look at what happens if you superimpose two shapes. You need to blend or *compose* the colors and alpha values of the source and destination pixels. Porter and Duff, two researchers in the field of computer graphics, have formulated 12 possible *composition rules* for this blending process. The Java 2D API implements all of these rules. Before going any further, we’d like to point out that only two of these rules have practical significance. If you find the rules arcane or confusing, just use the `SRC_OVER` rule. It is the default rule for a `Graphics2D` object, and it gives the most intuitive results.

Here is the theory behind the rules. Suppose you have a *source pixel* with alpha value a<sub>S</sub>. In the image, there is already a *destination pixel* with alpha value a<sub>D</sub>. You want to compose the two. The diagram in Figure 11.22 shows how to design a composition rule.

![](bbox=[0.36, 0.633, 0.716, 0.821])

**Figure 11.22** Designing a composition rule