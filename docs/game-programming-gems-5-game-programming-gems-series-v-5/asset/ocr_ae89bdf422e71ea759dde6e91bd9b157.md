# Other Uses

Finding the eight vertices of the frustum was a huge task on the six planes approach due to the involvement of computing the intersection of three planes eight times which indeed is an expensive operation. However, this is very simple using the radar approach. Take a look at Figure 1.6.8.

![](bbox=[0.45, 0.23, 0.6, 0.5])

FIGURE 1.6.8 Computing the point A by adding NVector and RVector.

The position of point A can be computed by adding the two vectors marked in Figure 1.6.8. Computing the nVector is just a matter of multiplying the unit forward vector by the “near” value. Finding the R vector is a little trickier; it is just the right vector times a factor that comes from the following evaluation:

```
rFactor = tan(FOV / 2) = opposite side / adjacent side = factor / near

rFactor = factor / near

factor = rFactor · near
```

Therefore, the R vector is defined as rVector = Right · rFactor · near. Adding it to the near vector gives point A, and the same can be applied to get all eight points. Check the provided source for a full implementation.