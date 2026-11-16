| 53 | 52 | 51 | 53 | 52 | 51 | 53 | 50 | 51 |
|---|---|---|---|---|---|---|---|---|
| 49 | 50 | 49 | 51 | 40 | 41 | 39 | 41 | 40 |
| 48 | 47 | 12 | 12 | 18 | 19 | 16 | 15 | 20 |
| 46 | 41 | 12 | 12 | 19 | 20 | 17 | 15 | 16 |
| 45 | 42 | 12 | 15 | 18 | 17 | 19 | 17 | 18 |
| 46 | 44 | 43 | 44 | 41 | 16 | 18 | 20 | 19 |

Figure 8.26 An image with three drains marked with shading, including the 5-pixel drain with brightness of 12, the 2-pixel drain with brightness of 15, and the 1-pixel drain with brightness of 16.

detector. This emphasizes the need for something additional. Perhaps a hybrid approach that could combine information from edges with region differences?

The concept introduced by Chan and Vese of describing the foreground (or interior) and the background (or exterior) by statistics continues to be a powerful idea. For example, Ramudu et al. [8.40] follow the same philosophy, but introduce a force (which they call an spf) equal to

```
spf(f(x, y)) = \frac{f(x, y) - \frac{1}{2}(\mu_1 + \mu_2)}{\max(f(x, y) - \frac{1}{2}(\mu_1 + \mu_2))} (8.60)
```

and show that using this force to move the contour often produces even better segmentations than Chan-Vese.

# 8.6 Watersheds: Segmentation Based on Brightness Surface

In this section, you will learn to think about moving up and down the brightness surface as water would move. We continue to consider the brightness function f(x, y) as if f represented vertical distance, and the brightness image is thought of as a surface.

Suppose we pour water onto that surface. Water runs downhill, and (assuming it isn't absorbed or evaporated) will eventually come to rest at some place that is a minimum of local elevation. In a digital (sampled and quantized) image, such a minimum is not necessarily a single pixel. It could be a set of neighboring pixels, all of which have the same brightness. We call that final, lowest set of points a drain. In general, there are many drains in an image. Given a single point (x, y) on the surface, place a single drop of water on the surface at that point, and follow it until it comes to rest at some drain. The collection of all surface points that flow to a single drain, say drain i, is referred to as the basin or catchment basin associated with that drain.

Some surprising problems occur when attempting to use basins to segment images. First, from a single point, water will flow in the direction of steepest slope, but it is certainly possible that there might be equal, steepest slopes in more than one direction. So the problem of tracking where that one drop of water flows could be challenging and have high computational complexity. But, instead of following water as it flows down, let's instead start at the drain, and find all the neighboring points that definitely flow into that drain. That calculation can be done locally. Then, we find the points that drain into those points, etc.

Figure 8.26 illustrates pixel brightnesses in the vicinity of a 5-pixel drain. Each pixel “looks at” its neighbors and says, “If you are my neighbor and are brighter than me, you