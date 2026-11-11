![](bbox=[0.12, 0.09, 0.55, 0.3])

*Figure 3.4: The point $P = (x, y, z)$ is on our object. The string from $P$ to the eye, $E$, will pass through the window frame at some location $P' = (x', y', z')$. Note that $z' = 1$, because we chose our coordinates to make that happen.*

![](bbox=[0.16, 0.43, 0.53, 0.59])

*Figure 3.5: Two similar triangles overlaid on the picture in the $x = 0$ plane. The vertical edges of the small red and large blue triangles have lengths $y'$ and $y$, respectively. What are the lengths of their horizontal edges?*

We now know how to find the coordinates of $P'$ from those of $P$ in general! So we can describe our revised algorithm as shown in Listing 3.2.

*Listing 3.2: Simple-implementation version of the Dürer rendering algorithm.*

```
```
Input: a scene containing some objects
Output: a drawing of the objects

initialize drawing to be blank
foreach object o
    foreach visible point P = (x, y, z) of o
        if x_min <= (x/z) <= x_max and y_min <= (y/z) <= y_max
            make a point on the drawing at location (x/z, y/z)
```
```

Let's pause for a moment to examine this; We've now got the $x$- and $y$-coordinates of the pencil marks in the picture plane. But if we are to view the eventual picture from the location of the screw eye in the wall, the direction of