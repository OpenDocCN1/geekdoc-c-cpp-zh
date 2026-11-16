![](bbox=[0.186, 0.113, 0.792, 0.447])

Figure 10.15 Two Gaussian distributions are illustrated, one with a mean of 2.5, and another with mean of 7. The two distributions have significantly different variances. The point x = 4 is closer to the mean of class 1 (with a distance of 1.5) than to the mean of class 2 (with a distance of 3), yet at x, the probability is higher that x is in class 2.

uniformly sampled. This requires resampling of the boundary, which in turn prohibits boundary points from falling exactly on pixel boundaries. Figure 10.16 illustrates a simple way to resample a boundary.

If the resampled interval is 1.0, then the number of new sample points will be equal to the perimeter of the region. In addition to making measures of perimeter consistent, arc length parameterization also provides a great deal of power to curve representations, which you will learn when you take a course in differential geometry (which is another of the courses advanced students in computer vision should definitely take).

# 10.6.1 The Shape Matrix

Consider the boundary of some region in an image. Write every point on that boundary as a 2-vector of the form [x; y]. Assuming the boundary contains n points, the entire boundary can be written as a matrix of these vectors

```
X = [x1 ... xi ... xn; y1 ... yi ... yn]. (10.59)
```

For now, forget that this was the boundary of some region, and just think of it as a matrix representation for the shape X.