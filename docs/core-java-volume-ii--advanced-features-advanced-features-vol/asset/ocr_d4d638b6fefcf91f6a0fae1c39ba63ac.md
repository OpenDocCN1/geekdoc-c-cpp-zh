![](bbox=[0.344, 0.14, 0.743, 0.252])

**Figure 11.51** Overlaying a partially transparent rectangle on an image

Now let us look at what happens if you superimpose two shapes. You need to blend or **compose** the colors and alpha values of the source and destination pixels. Porter and Duff, two researchers in the field of computer graphics, have formulated 12 possible *composition rules* for this blending process. The Java 2D API implements all of these rules. Before going any further, we'd like to point out that only two of these rules have practical significance. If you find the rules arcane or confusing, just use the `SRC_OVER` rule. It is the default rule for a `Graphics2D` object, and it gives the most intuitive results.

Here is the theory behind the rules. Suppose you have a *source* pixel with alpha value αₛ. In the image, there is already a *destination* pixel with alpha value αᴅ. You want to compose the two. The diagram in Figure 11.52 shows how to design a composition rule.

![](bbox=[0.397, 0.561, 0.686, 0.758])

**Figure 11.52** Designing a composition rule

Porter and Duff consider the alpha value as the probability that the pixel color should be used. From the perspective of the source, there is a probability αₛ that it wants to use the source color and a probability of 1 − αₛ that it doesn't care. The same holds for the destination. When composing the colors, let us assume that the probabilities are independent. Then there are four cases, as shown in Figure 11.52. If the source wants to use the source color