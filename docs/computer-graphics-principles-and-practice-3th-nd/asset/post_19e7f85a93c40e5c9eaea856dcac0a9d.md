
## Chapter 11 Transformations in Three Dimensions

### 11.1 Introduction

Transformations in 3-space are in many ways analogous to those in 2-space.

- Translations can be incorporated by treating three-dimensional space as the subset $E^3$ defined by $w=1$ in the four-dimensional space of points $(x,y,z,w)$. A linear transformation whose matrix has the form

  $$\begin{bmatrix} 1 & 0 & 0 & a \\ 0 & 1 & 0 & b \\ 0 & 0 & 1 & c \\ 0 & 0 & 0 & 1 \end{bmatrix},$$

  when restricted to $E^3$, acts as a translation by $[a\quad b\quad c]^\mathsf{T}$ on $E^3$.

- If $T$ is any continuous transformation that takes lines to lines, and $\mathbf{O}$ denotes the origin of 3-space, then we can define

  $$\bar{T}(\mathbf{x}) = T(\mathbf{x}) - T(\mathbf{O}) \tag{11.1}$$

  and the result is a line-preserving transformation $\bar{T}$ that takes the origin to the origin. Such a transformation is represented by multiplication by a $3 \times 3$ matrix $\mathbf{M}$. Thus, to understand line-preserving transformations on 3-space, we can decompose each into a translation (possibly the identity) and a linear transformation of 3-space.

- Projective transformations are similar to those in 2-space; instead of being undefined on a line, they are undefined on a whole plane. Otherwise, they are completely analogous.

- Scale transformations can again be uniform or nonuniform; those that are nonuniform are characterized by three orthogonal invariant directions and three scale factors rather than just two, but nothing else is significantly different. The matrix for an axis-aligned scale by amounts $a, b,$ and $c$ along the $x$-, $y$-, and $z$-axes, respectively, is

will be sent to infinity exactly if, after transformation, its w-coordinate is zero, that is, if

\[ Ax + By + Cz + D = 0. \qquad (11.7) \]

That equation defines a plane in 3-space.

**Inline Exercise 11.2:** In the case described above in which a projective transformation is actually affine, which points in xyz-coordinates form the “plane sent to infinity”? It’s important to include \(w\) in your computation.

### 11.2 Rotations

Rotations in 3-space are much more complicated than those in the plane, but much of that complexity is of little significance for the casual user. We therefore present the essentials in this section, but we provide a much longer discussion of rotations in the web materials for this chapter.

We begin with some easily derived formulas that you’re likely to use often. Then we’ll discuss how to use notions like pitch, roll, and yaw (which are called Euler angles) to describe rotations, and how to describe a rotation by giving an axis of rotation and an angle through which to rotate (Rodrigues’ formula), as well as how to find the axis and angle for a rotation (a computation that’s also due to Euler). Both of these descriptions of rotations have limitations that make them unsuitable for interpolating between rotations, so we’ll consider a third way to describe rotations: To each point q of the sphere S³ in four-dimensional space R⁴ we can associate a rotation K(q) in a very natural way. There’s a small problem, however: The points q and −q of S³ correspond to the same rotation, so our correspondence is two-to-one. It turns out still to be easy to use this description of rotations to perform interpolation.

#### 11.2.1 Analogies between Two and Three Dimensions

Rotations in two dimensions given by matrices of the form

\[ \begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix} \qquad (11.8) \]

generalize nicely to three dimensions and higher. For instance, we can take the matrix for rotation through the angle θ in two dimensions and expand it to get

\[ R_{xy}(\theta) = \begin{bmatrix} \cos\theta & -\sin\theta & 0 \\ \sin\theta & \cos\theta & 0 \\ 0 & 0 & 1 \end{bmatrix}, \qquad (11.9) \]

which is the rotation by angle θ in the xy-plane of 3-space. As we mentioned in Chapter 10, this is also sometimes called rotation about z by the angle θ. The advantage of calling it rotation in the xy-plane is that there is an easy mnemonic associated to it: For small values of θ, the unit vector in the x-direction is rotated toward the unit vector in the y-direction. Corresponding statements are true of $R_{yz}$ and $R_{zx}$, which are written below. There’s another advantage: While rotations in 3-space always have an axis (see the web material for a proof) those in 2-space do not (e.g., there’s no vector in $\mathbb{R}^2$ left invariant by rotation through 30°), and neither do those in 4-space. But in all cases rotations can be described in terms of planes of rotation.

The analogous rotations in the $yz$- and $zx$-planes are given by

$$R_{yz}(\theta)=\begin{bmatrix}1&0&0\\0&\cos\theta&-\sin\theta\\0&\sin\theta&\cos\theta\end{bmatrix}\quad\text{and}\quad R_{zx}(\theta)=\begin{bmatrix}\cos\theta&0&\sin\theta\\0&1&0\\-\sin\theta&0&\cos\theta\end{bmatrix},$$
(11.10) and (11.11)

which can also be called rotation about $x$ and rotation about $y$, respectively.

In contrast to the two-dimensional situation, where we found that the set of $3\times3$ rotation matrices were one-dimensional, in three dimensions the set $SO(3)$ of $3\times3$ rotation matrices is three-dimensional. It is not, however, just a three-dimensional Euclidean space. One way to see it’s three-dimensional is to find a mostly one-to-one mapping from an easy-to-understand three-dimensional object to $SO(3)$ (just as the latitude-longitude parameterization of the 2-sphere shows us that the 2-sphere is two-dimensional). We’ll actually describe three such mappings, each with its own advantages and disadvantages. The first of these mappings is through **Euler angles**. This mapping is “mostly one-to-one,” in much the same way that the mapping of latitude and longitude to points on the globe is mostly one-to-one: Each point on the international date line has two longitudes (180E and 180W), and each pole has infinitely many longitudes, but each other sphere point corresponds to a single latitude-longitude pair.

#### 11.2.2 Euler Angles

**Euler angles** are a mechanism for creating a rotation through a sequence of three simpler rotations (called roll, pitch, and yaw). This decomposition into three simpler rotations can be done in several ways (yaw first, roll first, etc.); unfortunately, just about every possible way is used in some discipline. You’ll need to get used to the idea that there’s no single correct definition of Euler angles.

The most commonly used definition in graphics describes a rotation by Euler angles $(\phi,\theta,\psi)$ as a product of three rotations. The matrix $\mathbf{M}$ for the rotation is therefore a product of three others:

$$\mathbf{M}=R_{yz}(\psi)R_{zx}(\theta)R_{xy}(\phi).$$ (11.12)

Thus, objects are first rotated by angle $\phi$ in the $xy$-plane, then by angle $\theta$ in the $zx$-plane, and then by angle $\psi$ in the $yz$-plane. The number $\phi$ is called pitch, $\theta$ is called yaw, and $\psi$ is called roll. If you imagine yourself flying in an airplane (see Figure 11.1) along the $x$-axis (with the $y$-axis pointing upward) there are three direction changes you can make: Turning left or right is called yawing, pointing up or down is called pitching, and rotating about the direction of travel is called rolling. These three are independent in the sense that you can apply any one without the others. You can, of course, also apply them in sequence.

![](img/f464cd0043eb5336aa0543fe20a0561b_318_0.png)

*Figure 11.1: An airplane that flies along the x-axis can change direction by turning to the left or right (yawing), pointing up or down (pitching), or simply spinning about its axis (rolling).*

Writing this out in matrices, we have

$$\mathbf{M}=\begin{bmatrix}1&0&0\\0&\cos\psi&-\sin\psi\\0&\sin\psi&\cos\psi\end{bmatrix}\begin{bmatrix}\cos\theta&0&\sin\theta\\0&1&0\\-\sin\theta&0&\cos\theta\end{bmatrix}\begin{bmatrix}\cos\phi&-\sin\phi&0\\\sin\phi&\cos\phi&0\\0&0&1\end{bmatrix} \tag{11.13}$$

$$=\begin{bmatrix}\cos\theta\cos\phi&-\cos\theta\sin\phi&\sin\theta\\ *&*&-\sin\psi\cos\theta\\ *&*&\cos\psi\cos\theta\end{bmatrix}. \tag{11.14}$$

With the proper choice of $\phi$, $\theta$, and $\psi$, such products represent all possible rotations. To see this, we’ll show how to find $\phi$, $\theta$, and $\psi$ from a rotation matrix **M**. In other words, having shown how to convert a $(\phi,\theta,\psi)$ triple to a matrix, we’ll show how to convert a matrix **M** to a triple $(\phi',\theta',\psi')$, a triple with the property that if we convert it to a matrix, we’ll get **M**.

The $(1,3)$ entry of **M**, according to Equation 11.14, must be $\sin\theta$, so $\theta$ is just the arcsine of this entry; the number thus computed will have a non-negative cosine. When $\cos\theta\ne 0$, the $(1,1)$ and $(1,2)$ entries of **M** are positive multiples of $\cos\phi$ and $-\sin\phi$ by the same multiplier; that means $\phi=\operatorname{atan2}(-m_{21},m_{11})$. We can similarly compute $\psi$ from the last entries in the second and third rows. In the case where $\cos\theta=0$, the angles $\phi$ and $\psi$ are not unique (much as the longitude of the North Pole is not unique). But if we pick $\phi=0$, we can use the lower-left corner and atan2 to compute a value for $\psi$. The code is given in Listing 11.1, where we are assuming the existence of a $3\times3$ matrix class, `Mat33`, which uses zero-based indexing. The angles returned are in radians, not degrees.

*Listing 11.1: Code to convert a rotation matrix to a set of Euler angles.*

```
void EulerFromRot(Mat33 m, out double psi,
                  out double theta,
                  out double phi)
{
    theta = Math.asin(m[0,2]); //using C# 0-based indexing!
    double cos_theta = Math.cos(theta);
    if (Math.abs(cos_theta) == 0) {
        phi = 0;
    }
```
