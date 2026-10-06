
matching pair of keypoints, the RANSAC paradigm is used to compute the epipolar geometry constraint of fundamental matrix and set up the homography matrix.

The RANSAC procedure is opposite to that of conventional smoothing techniques: Rather than using as much of the data as possible to obtain an initial solution and then attempting to eliminate the invalid data points, RANSAC uses as small an initial dataset as feasible and ensures with consistent data when possible. For instance, given the task of fitting an arc of a circle to a set of 2D points, the RANSAC approach would be to select a set of three points, compute the center and radius of the implied circle, and count the number of points that are close enough to circle to suggest their compatibility with it (i.e, their deviations are small enough to measurement errors). If there are enough compatible points, RANSAC would employ a smoothing technique, such as least squares, to compute an improved estimate for the parameters of the circle now that a set of mutually consistent points has been-identified.

The formal RANSAC procedure is stated as follows:

- 1. Given a model that requires a minimum of $n$ data points to instantiate its parameters, and a set of data points $P$ such that the number of points in $P$ is greater than $\#(P) \ge n$ randomly select a subset $S1$ of $n$ data points from $P$ and instantiates the model. Use the instantiated model $M1$ to determine the subset $S1^*$ of points in $P$ that are within some error tolerance of $M1$. The set $S1^*$ is called the consensus set of $S1$.

- 2. If $\#(S1^*)$ is greater than some threshold $T$, which is a function of the estimate of the number of errors in $P$, use $S1^*$ to compute (possibly using least squares) a new model $M1^*$.

- 3. If $\#(S1^*)$ is less than $t$, randomly select a new subset $S2$ and repeat the above process. If, after some predetermined number of trials, no consensus set with $t$ or more members has been found, either solve the model with the largest consensus set found or terminate in failure.

The RANSAC paradigm contains three unspecified parameters: (1) the error tolerance used to determine whether a point is compatible with a model, (2) the number of subsets to try, and (3) the threshold $T$, which is the number of compatible points used to imply that the correct model has been found. In Section 11.2.3, we will discuss how RANSAC is applied to eliminate spurious matching pairs.

## 11.2.3 Geometric Consistency Test

We now have a set of putative matching image pair (I,J), and for each matching image pair, a set of individual feature matches. Because the matching procedure is imperfect: Many of these matches—both image matches and individual feature matches—will be spurned. Fortunately, it is possible to eliminate many spurious matches using a geometric consistency test. This test is based on the fact that, no matter what the actual shape of the scene is, there is a fundamental constraint between two perspectives of the static scene by the possible configurations of the two cameras and their corresponding epipolar geometry. In this section, we will first introduce the principle of projective geometry and derive the formula of computing the fundamental matrix F and the homography matrix H. Then we will discuss the procedure of computing F and H using RANSAC paradigm.

### 11.2.3.1 Projective Geometry and Transform

In the Exception of IR², the parallel lines will never meet in a single point. In order to escape from the exception, the projective geometry is proposed. In the projective plane IP², one may state without qualification that two distinct lines meet in a single point and two distinct points lie on a single line.

#### 11.2.3.1.1 The 2D Projective Plane A line in the plane is represented by an equation such as ax+by+c=0, with different choice of a, b, and c rise to different lines. Thus a line can be represented by the vector (a,b,c)ᵀ. Also, since (ka+kb+kc)=0, the vector (a,b,c)ᵀ is the same as k(a,b,c)ᵀ. After defining the lines, a point x=(x,y)ᵀ lies on the line ℓ=(a,b,c)ᵀ if and only if ax+by+c=0. This can be represented by (x,y,1)ᵀ. Points are presented by homogeneous vectors. An arbitrary homogeneous vector representative of a point is:

```
x = (x,y,z)ᵀ
```

- The point x lies on the line l if and only if xᵀℓ=0
- The line l through two points x and x is l=x×

#### 11.2.3.1.2 Ideal Points and the Line at Infinity Consider two lines ax+by+c=0 and ax+by+c'=0. These are presented by vectors l1=(a,b,ρ) and l2=(a,b,ρ') for the first two coordinates are the same. The intersection is l∩l2=(c,-c)(-a,0), and ignoring the scale (c,-c). Now may the inhomogeneous representation of this point (b,-a,0) makes no sense, except to suggest that the point of intersection has infinite coordinates. This observation agrees with the usual idea that parallel lines meet at infinity.

Now we may have the definition of ideal point that has the last coordinate xi=0 The set of all ideal points may be written as (x1,x2,0). Note that this set lies on a single line, the line at infinity, denoted by the vector 1=(0,0,1), since (0,0,1)(x1,x2,0)=0.

### 11.2.3.1 Projective Transformations 2D projective geometry is the study of properties of the projective plane IP² which are invariant under a group of transformations known as projectivity, which is an invertible mapping h from IP² to itself such that points p1, p2, and p3 lie on the same line if not h(p1), h(p2), and h(p3) do at infinity.

A planar transformation is a linear transformation on homogeneous four-vectors represented by a nonsingular 3×3 matrix:

```
$$\begin{pmatrix} \hat{A}_{11} & \hat{A}_{12} & \hat{A}_{13} \\ \hat{A}_{21} & \hat{A}_{22} & \hat{A}_{23} \\ \hat{A}_{31} & \hat{A}_{32} & \hat{A}_{33} \end{pmatrix} (11.1)$$
```

Or more briefly, x=Hx.

Note that the matrix H in this equation may be changed by multiplication by an arbitrary nonzero-scale factor without altering the projective transformation. Consequently, we say that H is a homogeneous matrix.

#### 11.2.3.1.4 Projective 3D Geometry Similar to 2D Geometry plane, point X is represented in homogeneous coordinates as a four-vector. Specifically, the homogeneous vector X=(x1,x2,x3,x4)ᵀ with x4!=0 representing the points at finite position while x4=0 representing the points at infinity.

A plane in three-space may be written as

```
$p1X+p2Y+p3Z+p4=0 (11.2)$
```

Clearly this equation is unaffected by multiplication by a nonzero-scale factor and the homogeneous representation of the plane is the four-vector $\mathfrak{p} = (\mathfrak{p}_1, \mathfrak{p}_2, \mathfrak{p}_3, \mathfrak{p}_4)^T$

Also we may have $\mathfrak{p}^T X=0$, which expresses that the point $X$ is on the plane $p$. It is easy to find that the first three components of the plane correspond to the normal plane of Euclidean geometry. This formula also be written as

```
$(\mathfrak{p}_1, \mathfrak{p}_2, \mathfrak{p}_3)^T(x_1, x_2, x_3)^T+d=0 \quad (11.3)$
```

where:
d=\pi_4$

## 11.2.3.2 Camera Model

A camera is a mapping between the 3D world (object space) and the 3D image. The principal plane of interest here is central projection.

### 11.2.3.2.1 The Basic Pinhole Model We consider the central projection of points onto a plane. The center of projection is the origin of a Euclidean coordinate system, and consider the plane $Z=f$, which is called image plane or focal plane. In this model, a point $X=(X, Y, Z)^T$ is mapped to the point on the image plane where a line joining the point $X$ to the center of projection meets the image plane. Ignoring the final image coordinate, we use that $(X, Y, Z)^T (fX/z, fY/z, fZ/z)^T$. This is a mapping from Euclidean three-space to two-space. The mapping can be represented by homogeneous vectors as

$$\begin{array}{ccccccc} \mathfrak{E} & & & & & \mathfrak{E} & \mathfrak{A}_x & \mathfrak{E}x & \mathfrak{E}f & & & & \ \mathfrak{A}_y & \mathfrak{E}y & & f & & & (11.4) \\ & & \mathfrak{A}_z & & \mathfrak{I} & & & & & & \ & \mathfrak{A}_z & & & & & & \ \mathfrak{A11 & 1 & & & \end{array}$}$

Or more briefly, $m=K\mathbf{0}X$, where $m=(x,y)^T$ and $K=\text{diag}(f,f)$. Because in Reference 1, the author believes that all the principal points are in the center of image plane, there is no need to find the principal point.

#### 11.2.3.2.2 Camera Rotation and Translation

In general, points will be expressed in terms of a different Euclidean coordinate frame, known as
