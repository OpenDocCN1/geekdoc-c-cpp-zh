can be easily handled by the level set function, but cannot be handled by particle-based methods.

```
\psi(x, y) = 1.5e^{-2((x+0.5)^2+(y-0.1)^2)} + e^{-2((x-0.1)^2+(y-0.1)^2)} - 1 \quad (8.33)
```

The idea is this: define a function whose zero level set is the initial contour, which we get to choose. The zero level set naturally results in a segmentation of the image with two regions defined as \(\psi(x, y) \ge 0\) and \((\psi(x, y) < 0)\). Then modify that function in such a way that its zero level set moves in the desired direction.

In practice, there are many functions of x and y that can be used. For example, we can interpret the thresholding-based segmentation methods in the context of level sets, where the level set function can be defined as the value of the grayscale image, i.e., \(\psi(x, y) = f(x, y) - t\) with t being the threshold. Hence, the segmentation result is such that \(\{\psi(x, y) \ge 0\}\) (or \(\{f(x, y) \ge t\}\)) is thought of as one region and \(\{\psi(x, y) < 0\}\) (or \(\{f(x, y) < t\}\)) as another region. Another convenient way to define the initial contour is to use the distance transform as illustrated here.

Do you remember the distance transform? In Chapter 7, the distance transform resulted in a function DT(x, y) that was equal to zero on boundary pixels and got larger as one moved away from the boundary. Now consider a new version of the distance transform, which is exactly the same as the old one outside the contour of interest. (Remember, the contour is closed, and so the concepts of INSIDE and OUTSIDE make sense.) Inside the contour, this new function (which we will refer to as the metric function) is the negative of the distance transform.

```
\psi(x, y) = \begin{cases} DT(x, y), & \text{if } (x, y) \text{ is outside the contour} \\ -DT(x, y), & \text{if } (x, y) \text{ is inside the contour} \end{cases} \quad (8.34)
```

Level set-based segmentation algorithms modify the metric function \(\psi\). For every point (x, y) we compute a new value of \(\psi(x, y)\), according to some modification rule. There are several ways we could modify those points, and we will discuss two of them below. One moves the contour using image edges, and the other moves the contour without using image edges. Remember that the contour of interest is still the set of points where the (modified) metric function takes on a value of zero, i.e., the zero level set. We initialize it to be the distance transform or other function of x and y. This is another advantage of the level set-based segmentation method where the initial contour does not have to be very close to the actual edge of the region of interest.

In this section, several things are related: the metric function, \(\psi\), its zero level set, which is the contour, the motion of the contour, and the change in \(\psi\) required to result in a motion of contour. The expressions zero level set and contour are used interchangeably here. We will use the vector representation of spatial coordinates, x = [x y]^T.

# Moving the Contour using Image Edges

Consider a point x in the zero level set, and observe that at any time t, \(\psi\) is a function of three variables,

```
\psi(x, y, t). \quad (8.35)
```