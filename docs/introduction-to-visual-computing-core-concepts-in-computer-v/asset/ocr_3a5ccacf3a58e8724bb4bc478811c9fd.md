projection transformation to also convert the truncated pyramidal view frustum into a cuboid that extends in each of the X, Y, and Z direction from −1 to +1. This is illustrated in Figure 13.4. In order to illustrate this transformation, consider the point $P_v = R(N,V)T(-E)MP = (X,Y,Z)^T$ where $P_v$ denotes the vertex after model and view transformation.

![](bbox=[0.192, 0.229, 0.582, 0.414])

**Figure 13.4.** This shows the transformation from the truncated canonical frustum to the cuboid shaped frustum as part of the perspective projection.

The first step is to coincide the general gaze direction to the default gaze direction that coincides with the normal to the image plane when the viewport is such that $l=-r$ and $b=-t$. This is achieved by a shear that brings the point $((l+r)/2,(t+b)/2,n)$ to $(0,0,n)$. Since the $z$ coordinate remains unchanged, this transformation is a $Z$ shear. Let the parameters of this shear be $(a,b)$. Therefore,

$$\begin{pmatrix}0\\0\\n\\1\end{pmatrix}=\begin{pmatrix}1&0&a&0\\0&1&b&0\\0&0&1&0\\0&0&0&1\end{pmatrix}\begin{pmatrix}(l+r)/2\\(t+b)/2\\n\\1\end{pmatrix} \tag{13.5}$$

From this we can find the parameters $a$ and $b$ of shear to be

$$a=-\frac{l+r}{2n} \tag{13.6}$$

$$b=-\frac{t+b}{2n} \tag{13.7}$$

Therefore, the first matrix for perspective projection of $P_v$ is $Sh_z(-\frac{l+r}{2n},-\frac{t+b}{2n})$ and it provides the transformation to account for the off-axis viewport.

The next step is to transform the view frustum from a truncated pyramid to a cuboid. Let us assume, for the moment, that the $z$ coordinate does not matter since after projecting to the image plane, all the vertices will have the depth $n$. We will revisit the depth issue later. Therefore, if $z$ coordinate is ignored, the goal is to map the viewport which extends from $l$ to $r$ in the $x$ direction to −1 to +1 in the $x$ direction, and from $t$ to $b$ in the $y$ direction to −1 to +1 in $y$ direction. This means that lengths of $r-l$ horizontally and $t-b$ vertically should be mapped to 2. Since the center is already at $(0,0)$ following the shear, this can be achieved by a scaling transformation $S(\frac{2}{r-l},\frac{2}{t-b},1)$. Therefore, the complete transformation until this step for a vertex $P_v$ is given by $P_s=S(\frac{2}{r-l},\frac{2}{t-b},1)Sh_z(-\frac{l+r}{2n},-\frac{t+b}{2n})P_v$.