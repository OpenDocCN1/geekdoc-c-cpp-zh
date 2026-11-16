![](bbox=[0.45, 0.08, 0.7, 0.3])

FIGURE 1.6.3 A two dimensional frustum is represented as an isosceles triangle where the height matches the forward vector.

directly but the tangent of that angle; so that is the only thing that must be computed when building the frustum. Even that, though, can be cached and only computed when the camera changes the FOV (which, in most games, only occurs when a zoom is performed, changing the perspective. While that angle remains unchanged, the frustum is built by copying the forward and right vectors directly from the camera. This is far cheaper than performing all the calculations required to build a frustum using the six planes approach. And now, let's go to the really interesting part: knowing if something is inside the frustum.

# Is a Point Inside a Frustum?

First, let's see what we need for knowing if a given point is inside the frustum; check Figure 1.6.4. To know if the point P is in the frustum, the radar approach projects OP to the forward and right vectors. The point P is known to be in the frustum if the forward projection F is between the far and near values and the right projection R is between rLimit and -rLimit; otherwise, it is meant to be completely out.

As described earlier, the first thing that must be done is to compute the projections F and R. To project one vector into another, a dot product is performed and the resulting scalar is multiplied by either of the two vectors to obtain the projection in the desired axis. Figure 1.6.5 illustrates. There are two vectors V1 and V2, and the dot product of them returns a scalar s.

```
s = V1 dot V2 = V1 • V2 = V2.x * V1.x + V2.y * V1.y
```