
where Z0 and Z1 are the depths of A and B respectively from the view point. The image plane is represented by the red line. The projection of the line on this image plane would be given by 1D coordinates s0 and s1. These are called the screen space coordinates of the 3D primitive. Let us assume that we have stored the depth of these two projected vertices - Z0 and Z1.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_316_0.png)

Let us now consider the future stage of scan conversion where we are interpolating the attributes of a point half-way between s0 and s1 in screen coordinates, i.e. (s0+s1)/2. Therefore, we will compute the depth of this point using the same interpolation coordinates as (Z0+Z1)/2. However, the depth of the object point C that is projected at the screen coordinate (s0+s1)/2 is not (Z0+Z1)/2. The green curve in the object space in Figure 13.6 plots the depth computed through linear interpolation in the screen space. e shows the difference between the actual depth and the linearly interpolated depth in the screen space. Of course, the shape of the green curve and the amount of error will change based on the exact positions of A and B.

Figure 13.5. The shows two intersecting triangles viewed from a the shown view direction. The orange regions shows the visible parts of each triangle from this view direction which should be rendered after occlusion resolution.

Therefore, the question is what kind of interpolation would yield the correct result? For this, let us consider the point (Xt, Zt) between A and B defined by the interpolation coefficient t in 3D. Therefore,

```
Xt = X0 + t(X1 − X0)    (13.13)
Zt = Z0 + t(Z1 − Z0)    (13.14)
```

Let their projection on the image plane be between s0 and s1 defined by the 2D interpolation coefficient u, su. Therefore,

```
su = s0 + u(s1 − s0) = X0/Z0 + u( X1/Z1 − X0/Z0 )    (13.15)
```

Since su is the image of (Xt, Zt), we can derive the following.

```
su = Xt / Zt    (13.16)
```

```
Or,  X0/Z0 + u( X1/Z1 − X0/Z0 ) = [X0 + t(X1 − X0)] / [Z0 + t(Z1 − Z0)]    (13.17)
```

To achieve this, we have to map \(\frac{1}{n}\) to \(-1\), \(\frac{1}{f}\) to \(+1\), and the center of the range \([\frac{1}{n},\frac{1}{f}]\) to 0. The center is given by

$$\frac{\frac{1}{f}+\frac{1}{n}}{2}=\frac{f+n}{2nf}.$$  \tag{13.27}

This movement of the center is achieved by a translation by \(-\frac{f+n}{2nf}\). Then, the extent between \(\frac{1}{n}\) to \(\frac{1}{f}\) is scaled to 2 via a scale factor of

$$\frac{2}{\frac{1}{f}-\frac{1}{n}}=\frac{2nf}{n-f}.$$  \tag{13.28}

Therefore the final expression for the third coordinate of \(P_l\) is given by

$$\left(\frac{1}{Z_v}-\frac{f+n}{2nf}\right)\frac{2nf}{n-f}=\frac{2nf}{(n-f)Z_v}+\frac{f+n}{f-n}=\frac{\frac{2nf}{n-f}-\frac{n+f}{n-f}Z_v}{Z_v}.$$  \tag{13.29}

Therefore, \(P_l\) that we would like to achieve is given by

$$\begin{pmatrix}\frac{2X_vn}{Z_v(y-r_l)}-\frac{l+r}{r-l}\\\frac{2Y_vn}{Z_v(b-t)}-\frac{t+b}{t-b}\\\frac{Z_v(b-t)}{2nf}+\frac{n+f}{n-f}Z_v\\1\end{pmatrix}=\begin{pmatrix}\frac{2X_vn}{Z_v(y-r_l)}-\frac{l+r}{r-l}Z_v\\\frac{2Y_vn}{Z_v(b-t)}-\frac{t+b}{t-b}Z_v\\\frac{2nf}{n-f}+\frac{n+f}{n-f}Z_v\\Z_v\end{pmatrix}.$$  \tag{13.30}

This can be achieved by making \(D(n)\) into a matrix that depends on both \(n\) and \(f\) and is given by

$$D(n,f)=\begin{pmatrix}n&0&0&0\\0&n&0&0\\0&0&-\frac{n+f}{n-f}&\frac{2nf}{n-f}\\0&0&1&0\end{pmatrix}.$$  \tag{13.31}

Therefore, the entire perspective projection matrix $L$, now dependent on $f$ also, is given by

$$D(n,f)S\left(\frac{2}{r-l},\frac{2}{t-b},1\right)Sh_z\left(-\frac{l+r}{2n},-\frac{t+b}{2n}\right)$$

$$=\begin{pmatrix} n&0&0&0\\0&n&0&0\\0&0&-\frac{n+f}{n-f}&\frac{2nf}{n-f}\\0&0&1&0\end{pmatrix}\begin{pmatrix}\frac{2}{r-l}&0&0&0\\0&\frac{2}{t-b}&0&0\\0&0&1&0\\0&0&0&1\end{pmatrix}\begin{pmatrix}1&0&-\frac{r+l}{2n}&0\\0&1&-\frac{t+b}{2n}&0\\0&0&1&0\\0&0&0&1\end{pmatrix}$$

$$=\begin{pmatrix}\frac{2n}{r-l}&0&0&0\\0&\frac{2n}{t-b}&0&0\\0&0&-\frac{n+f}{n-f}&\frac{2nf}{n-f}\\0&0&1&0\end{pmatrix}\begin{pmatrix}1&0&-\frac{r+l}{2n}&0\\0&1&-\frac{t+b}{2n}&0\\0&0&1&0\\0&0&0&1\end{pmatrix}$$

$$=\begin{pmatrix}\frac{2n}{r-l}&0&-\frac{r+l}{r-l}&0\\0&\frac{2n}{t-b}&-\frac{t+b}{t-b}&0\\0&0&-\frac{n+f}{n-f}&\frac{2nf}{n-f}\\0&0&1&0\end{pmatrix}$$

This matrix $L(n,f,r,l,t,b)$ is often called the frustum transformation matrix since it is dependent on the parameters that define the view frustum.

The top-left $3\times3$ submatrix of Equation 13.35 looks exactly like the intrinsic parameter matrix in Equation 7.10 where the focal length is $n$, the horizontal and vertical scale factors are $\frac{2}{r-l}$ and $\frac{2}{t-b}$ respectively and the horizontal and vertical offsets are $-\frac{l+r}{2}$ and $-\frac{t+b}{2}$ respectively. In other words, while the view transformation is essentially the extrinsic parameter matrix, the frustum transformation matrix $L$ is essentially the intrinsic parameter matrix. The camera model in the synthesis pipeline is essentially the same as the pinhole camera model, but we arrive at the same equations from different directions and use it differently.

## 13.1.5 Window Coordinate Transformation

The perspective transformation normalizes each of the three coordinates to be between −1 to +1. However, the final drawing in any image synthesis has to be done on a window on the display screen which is usually defined by integer coordinates of the top left and bottom right corner of the window. Therefore, this is exactly similar to providing the viewport. Let the coordinates of these top, left, right and bottom window be $t_w$, $l_w$, $b_w$ and $r_w$ respectively. Therefore, the center of the window is given by $\left(\frac{l_w+r_w}{2},\frac{t_w+b_w}{2}\right)$ and the length and height of the window is given by $r_w-l_w$ and $t_w-b_w$ respectively. The transformation to the window coordinates involve a translation by $\left(\frac{l_w+r_w}{2},\frac{t_w+b_w}{2}\right)$ and a scaling by

r_w - l_w / 2 and t_w - b_w / 2 in horizontal and vertical directions respectively while keeping the z-coordinate unaffected. This is achieved by the transformation

W(t_w, l_w, b_w, r_w) = \begin{pmatrix} \frac{r_w - l_w}{2} & 0 & 0 & \frac{l_w + r_w}{2} \\ 0 & \frac{t_w - b_w}{2} & 0 & \frac{t_w + b_w}{2} \\ 0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \end{pmatrix} (13.36)

## 13.1.6 The Final Transformation

Therefore the complete transformation G of a point P is given by

G = W(l_w, r_w, t_w, b_w) L(n, f, r, l, t, b) R(N, V) T(-E) M (13.37)

The above transformation projects the point from the object coordinate system to the window coordinates. This is exactly how the vertices a, b, c and d are generated in Figure 13.1 from the 3D vertices A, B, C and D.

## 13.2 Clipping and Vertex Interpolation of Attributes

Clipping is usually done in the graphics hardware and the application programmer does not need to worry about. Yet, we provide a very short overview here. Clipping is done in 2D following the projection of points. We will discuss some 3D clipping methods in later chapters. Any 2D clipping algorithm fundamentally depends on finding intersections of primitive (lines or polygons) with the edges of the window. Therefore, the mathematics behind these algorithms are straight forward. However, what makes it challenging in the context of the interactive graphics pipeline is its efficiency. Every primitive or triangle needs to go through the process of clipping and when the scene consists of millions of triangles efficiency of the algorithm becomes important even if it is done in the hardware. Following are some of the ways to increase the efficiency; they are most likely to be deployed one after the other in sequence.

## Fun Facts

![](img/66c45bbed85bb7ba7f7b05dff49b5060_322_0.png)

In computer graphics you will come across the *revered Utah teapot* model which has become synonymous to CG innovation ever since Martin Newell, a graduate student at the University of Utah, modeled and introduced the object to the computer graphics community. The actual teapot that Newall used to create the digital model resides at the Computer History Museum in Mountain View, California. So why a teapot? It is said that Newall’s wife suggested the object while the two were having tea. But her idea was perfect technically due to a large number of reasons cited over the years. It is round, has saddle points, has a non-zero genus due to the hole in the handle, can project a shadow on itself, can have a self-reflection, and looks reasonably aesthetic even when rendered without a texture. It is amazing that such a simple object provided computer graphics researchers with so much complexity so as to become the benchmark geometric model. In 2006, Professor Peter Shirley of the University of Utah paid homage to this model through his Siggraph Talk “The Teapot Through the Ages”. Each year at SIGGRAPH (the biggest conference for computer graphics academicians, industry and enthusiasts) Pixar hands out hundreds of tiny wind-up teapot to collectors.

Performing a number of floating point intersection operations for every primitive is definitely not the most efficient way to achieve clipping, especially when a large majority of triangles can fall either completely outside the window or completely inside it and only a few will actually intersect the window boundaries. One way to improve performance is to make sure that intersection computations are only performed when there is a high probability that the primitive actually intersects the window boundaries. Therefore, a fast acceptance or rejection test for primitives completely inside or outside the window is critical. Such tests can be achieved in multiple ways.

- *Using Bounding Boxes:* We can compute the axis aligned bounding box of each triangle and see if it lies completely inside or outside the window. An axis aligned bounding box is the smallest box enclosing the primitive, with sides parallel to the axes of the window. If this bounding box is completely outside, the primitive is rejected. If it is completely inside, it is accepted. An axis-aligned bounding box for each primitive can be computed by just finding the minimum and maximum extent of the vertices in the horizontal and vertical direction. Testing of this bounding box is also easily achieved without any intersection computation by checking for intersection between the extents of the bounding box and window. Only primitives whose bounding box intersects the window go through the intersection computation. In Figure 13.7, both the horizontal and
