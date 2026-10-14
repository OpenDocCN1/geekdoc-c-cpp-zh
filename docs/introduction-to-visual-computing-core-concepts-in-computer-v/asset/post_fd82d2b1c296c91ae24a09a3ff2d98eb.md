
$M = I M_u = M_u$. Interestingly, if $u_1$, $u_2$ and $u_3$ are known, this rotation matrix is simply given by plugging in these vectors as

$$M_u = \begin{pmatrix} u_1 \\ u_2 \\ u_3 \\ 0\quad 0\quad 0\quad 1 \end{pmatrix} \tag{6.55}$$

![](img/66c45bbed85bb7ba7f7b05dff49b5060_161_0.png)

**Figure 6.11.** This shows how to create a 3D coordinate system using a single vector $u_1$.

Let us relate this back to another situation we face when finding the matrix of rotation about an arbitrary axes. After we rooted the arbitrary axes to the origin, we could have used an alternate way to find the matrix that would align $u$ with one of the coordinate axes. We could have considered $u = u_3$ and created a coordinate system using $u_2 = u_3 \times (1,0,0)$ and $u_1 = u_3 \times u_1$. Then we could have put these vectors in the Equation 6.55 to generate the rotation matrix to align $u$ with $z$-axis. This matrix would be equivalent to what you achieved by $R_y(\beta)R_x(\alpha)$ in Equation 6.41 and its inverse given by $M_u^T$ will be exactly what you would achieve by $R_x(\alpha)^{-1}R_y(\beta)^{-1}$ in Equation 6.42. In other words, we can just define a coordinate system using the arbitrary axis and the vectors of this coordinate system will define the rotation matrix as one of the orthogonal axes computing $\alpha$ and $\beta$.

## 6.6 Properties of Concatenation

Now that we have learned about both coordinate systems and concatenation of transformations, we will now explore some relationships between them. We have already seen before that since concatenation of transformation is represented by matrix multiplication and since matrix multiplication is not commutative, the order in which we concatenate transformations is critical to arrive at the desired transformation.

However, though matrix multiplication is not commutative, it is associative. To understand the implication of this associative law, let us consider two different transformations $\mathcal{T}_1$, $\mathcal{T}_2$, and a point $P$. These transformations can be any linear transformation and so can be represented by a matrix. Now, due to the associative law, we can say that

$$\mathcal{T}_1\mathcal{T}_2P = (\mathcal{T}_1(\mathcal{T}_2P)) = ((\mathcal{T}_1\mathcal{T}_2)P) \tag{6.56}$$

The above equation says that it really does not matter if the multiplications are performed from the left to right or right to left i.e. $\mathcal{T}_1$ and $\mathcal{T}_2$ can be multiplied first and then the result post-multiplied by $P$ or $T_2$ and $P$ can be multiplied first and the result pre-multiplied by $T_1$ to get the same answer. Therefore, whether the multiplications are performed as a post or pre-multiplication does not really matter as long as their order is preserved. Though this may seem to be of trivial consideration, it has a rather deep geometric interpretation.

### 6.6.1 Global vs Local Coordinate System

The transformation $T_1T_2P$ transforms the point $P$ and whether it is done using pre-multiplication or post-multiplication, the result will be the same. However, the geometric interpretation of the intermediate steps are dependent on the pre or post multiplication.

So far, in this chapter, we have been doing concatenation as a pre-multiplication, i.e. pre-multiply $T_2$ with $P$ first and then pre-multiply the result with $T_1$. When we perform each of these steps we consider the coordinate system to be constant. Hence, the coordinate systems remain _global_ across the different transformations. This is usually easy to understand since we typically work with a standard frame of reference.

However, the post multiplication also has an interpretation. It means that the _coordinate system itself is being transformed_. Therefore when you post multiply $T_1$ with $T_2$, it means that you have first applied the transformation $T_1$ to the coordinate system followed by $T_2$ to the transformed coordinate system and then placed $P$ in this transformed coordinate system. Here, the coordinate system remains _local_ to each transformation and changes from one transformation to another.

However, the result of implementing the transformation both in global or local coordinates achieves the same result. To illustrate this, please see Figure 6.12. We consider the transformation $RTP$ in 2D for this object and perform it in both global and local coordinate systems to achieve the same result.

## 6.7 Projective Transformation

This brings us to the end of affine transformation. Now, we will explore projective transformation. Projective transformations are most general linear transformations which take points $P=(x,y,z,w)$ to points $P'=(x',y',z',w')$. Projective transform $P$ is expressed as

$$\begin{pmatrix}x'\\y'\\z'\\w'\end{pmatrix}=\begin{pmatrix}p_{11}&p_{12}&p_{13}&p_{14}\\p_{21}&p_{22}&p_{23}&p_{24}\\p_{31}&p_{32}&p_{33}&p_{34}\\p_{41}&p_{42}&p_{43}&p_{44}\end{pmatrix}\begin{pmatrix}x\\y\\z\\w\end{pmatrix} \tag{6.57}$$

Figure 6.12. We consider the transformation RTP in 2D for this object. Top: This shows the transformation performed in a global coordinate system, i.e. using pre-multiplication. Therefore, the object is first translated and then rotated. Bottom: This shows the transformation performed in a local coordinate system i.e. using post-multiplication. Therefore, the coordinate system is first rotated relative to its own coordinate system. The object will also change position due to this since its coordinates with respect to the local coordinate system have not changed. Next the coordinate system is translated relative to itself. The changing coordinates are shown in red. Note the final location of the object is the same which is due to the associative nature of matrix multiplication.

The most important difference of projective transformation is that it can take finite points to points at infinity. The implication of this is that non-parallel lines can become parallel and vice versa. However, it still does not change the degree of a curve. So, a line cannot become a curve. A circle can become an ellipse (none of its points go to infinity) or even a parabola (where some of its points go to infinity) but it cannot become a degree-3 polynomial. Please see exercise problems to check it for yourselves.

The most common projective transformation we face is when we deal with a camera. A camera projects the 3D objects in the world on a 2D image plane to create an image. The most basic camera model is called the pin-hole camera where the camera is considered to be a simple pinhole. Think of a box with a hole in one of its face and the opposite face acting as an imaging plane and voila! There we have a pin-hole camera as illustrated in Figure 6.13. Here O denotes the pinhole. Rays of light from 3D points A, B and C come through O and

![](img/66c45bbed85bb7ba7f7b05dff49b5060_163_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_164_0.png)

Figure 6.13. This shows a pinhole camera where O is the pinhole. Rays of light from 3D points A, B and C come through O and intersect the image plane behind it form their 2D image at A′, B′ and C′ respectively.

intersect the image plane behind it to form their 2D image at A′, B′ and C′ respectively under a projective transformation. It is important to note that such a projective transformation changes the size of the image based on the distance from the pinhole. For example, objects B and C appear to be of the same height in the image B′ and C′. However, B is double the size of C in 3D, but it is double distance away. Further, multiple points on the same ray will have the same image on the image plane therefore losing their depth information. We will explore the camera projective transformation in more details in the next chapter.

## 6.8 Degrees of Freedom

Degrees of freedom defines the number of parameters that can be changed during a transformation. Let us consider for example, a 2D rigid body transform. This will be represented by a 3 × 3 matrix when considering homogeneous coordinates. This is often referred to as the 3 × 3 homogeneous transformation. As you know, for rigid body transformation, the object can undergo only translation (2 parameters) or rotation (1 parameter). Therefore, this matrix has three degrees of freedom. This matrix will have the translation parameters on the last column and the rotation parameters will be used to fill the top left 2 × 2 sub-matrix. Therefore, though six entries of this matrix can be changed, they are not
