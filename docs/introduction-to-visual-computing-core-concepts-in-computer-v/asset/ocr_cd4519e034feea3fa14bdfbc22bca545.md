![](bbox=[0.177, 0.129, 0.8, 0.201])

**Figure 6.6.** Left: This shows an example of 2D shear. A square (a) undergoes a Y-shear to create the rhombus in (b). In Y-shear the y-coordinate remains unchanged while the x-coordinate gets translated proportional to the value of the y-coordinate. Therefore, all the points on the X-axis whose y-coordinate is 0 remain unchanged. But as the y-coordinate increases, the x-coordinate moves, in this example, towards the right, creating the shear. Similarly, (c) shows an X-shear. (d) shows the result of first applying a X shear followed by a Y shear. Therefore, the only unchanged point is the origin where both x and y coordinates are 0. Note that if the proportionality constant for the shear is negative, then the Y-shear will move the square to the left instead of right. Right: This shows an example of Z-shear in 3D where Z is the axis of the cylinder.

# 6.3.4  Shear

Shear is a transformation where one coordinate gets translated by an amount that is proportional to the other coordinate. **Figure 6.6** shows an example of 2D shear. The shear is identified by the coordinate that remains unchanged due to the shear. So, a Y-shear keeps the y-coordinate unchanged and translates the x-coordinate proportional to the y-coordinate.

The equations that describe the transformation of point $P$ to $P'$ due to a Y-shear is given by

$$x' = x + ay$$
$$y' = y$$

where $a$ is the parameter of the shear. Therefore, the shear matrix is given by

$$P' = \begin{pmatrix}x'\\y'\\1\end{pmatrix} = \begin{pmatrix}1 & a & 0\\0 & 1 & 0\\0 & 0 & 1\end{pmatrix}\begin{pmatrix}x\\y\\1\end{pmatrix} = \mathcal{H}_y(a)P$$

When extending this to 3D, two coordinates should be translated proportional to the third one. So, for Z shear, the z-coordinate remains unchanged while the x and y coordinates are translated proportional to z. However, the constant of proportionality can be different and therefore the shear matrix would have two parameters. The matrix for a 3D Z-shear is given by

$$P' = \begin{pmatrix}x'\\y'\\z'\\1\end{pmatrix} = \begin{pmatrix}1 & 0 & a & 0\\0 & 1 & b & 0\\0 & 0 & 1 & 0\\0 & 0 & 0 & 1\end{pmatrix}\begin{pmatrix}x\\y\\z\\1\end{pmatrix} = \mathcal{H}_z(a,b)P$$