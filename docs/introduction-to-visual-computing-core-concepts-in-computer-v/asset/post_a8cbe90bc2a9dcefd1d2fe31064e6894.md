
# Input Images

![](img/66c45bbed85bb7ba7f7b05dff49b5060_282_0.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_282_1.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_282_2.png)

![](img/66c45bbed85bb7ba7f7b05dff49b5060_282_3.png)

Recovered Reflectance

Recovered Normals

Recovered Shape

Figure 11.18. This figure shows the recovery of shape from illumination under the assumption that the object is Lambertian. The top row shows the five input images taken by changing only the light position. The bottom row shows the recovered reflectance function (left), the normals (middle) and the reconstructed shape (right).

simple illumination model considering a point light source from the direction L illuminating an object point P with normal N. More light is incident per unit area of the object if L and N are coincident i.e. the light is illuminating P head-on. As the angle between L and N increases, the amount of incident light decreases. It can be shown that the fall off of incident light per unit area is proportional to cosθ where θ is the angle between N and L. Therefore, the illumination at P is given by N · L. To compute the amount of the illumination that is reflected from P, we assume the object to be Lambertian i.e. reflects light equally in all directions. Let fraction of light reflected be ρ. Therefore, the amount of reflected light is given by ρ · N · L.

Now, for photometric stereo, let us consider a set up where a Lambertian object is being seen by a camera. The locations of both the object and the camera do not change. However, it is lighted by n lights located at different locations surrounding the object. These light directions are known and given by L1, L2, …, Ln, where Li is a vector given by (Li^x, Li^y, Li^z). Let the light intensities be unity. Let the point P with normal N = (n^x, n^y, n^z) and reflectance ρ on the object be seen at a camera location (p, q). Let the reflected illumination recorded by the camera at (p, q) with only light Li illuminating the surface be Ri(p, q). Therefore at each pixel (p, q)

R_i = ρ N · L_i. (11.6)

Expanding this, we get the following equation at each pixel $(p,q)$ for each light $L_i$.

$$R_i - \rho \begin{pmatrix} L_i^x & L_i^y & L_i^z \end{pmatrix} \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} = 0 \tag{11.7}$$

Taking into account all the $n$ lights we get

$$\begin{pmatrix} R_1 \\ R_2 \\ . \\ . \\ R_n \end{pmatrix} - \rho \begin{pmatrix} L_1^x & L_1^y & L_1^z \\ L_2^x & L_2^y & L_2^z \\ \cdots \\ \cdots \\ L_n^x & L_n^y & L_n^z \end{pmatrix} \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} = 0 \tag{11.8}$$

Rearranging the terms, we get

$$\begin{pmatrix} L_1^x & L_1^y & L_1^z \\ L_2^x & L_2^y & L_2^z \\ \cdots \\ \cdots \\ \cdots \\ L_n^x & L_n^y & L_n^z \end{pmatrix}^{-1} \begin{pmatrix} R_1 \\ R_2 \\ . \\ . \\ . \\ R_n \end{pmatrix} = \rho \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} \tag{11.9}$$

$$\text{or } \mathbf{L}^{-1}\mathbf{R} = \rho N \tag{11.10}$$

where $\mathbf{L}^{-1}$ is the pseudo-inverse of the non-square matrix $L$. Note that, at every pixel $(p,q)$ the light directions and the intensity recorded are known. Each term in the left hand side of the Equation 11.10 is known. Therefore, we compute the right hand side of the equation and the vector obtained is the normal vector at the point on the object scaled by $\rho$. The magnitude of this vector provide reflectance $\rho$ at $(p,q)$ and the corresponding unit vector provide the normal $N$. This is illustrated in Figure 11.18.

The above process gives us the surface normal at any pixel $(p,q)$ and its reflectance, but not its depth. So, in the next step we need to find the depth of the surface with respect to the camera. Let us consider the camera’s coordinate system and the surface as shown in Figure 11.19. Let the depth of points at $(p,q)$, $(p,q+1)$, and $(p+1,q)$ given by $z_{p,q}$, $z_{p+1,q}$ and $z_{p,q+1}$ respectively. Note that the tangent plane to the normal $N = (N_x, N_y, N_z)$ recovered by the photometric stereo can be approximated by the vectors $V_1$ and $V_2$, assuming a smoothly varying normal, and is given by

$$V_1 = (p+1, q, z_{p+1,q}) - (p, q, z_{p,q}) = (1, 0, z_{p+1,q} - z_{p,q}) \tag{11.11}$$

$$V_2 = (p, q+1, z_{p,q+1}) - (p, q, z_{p,q}) = (0, 1, z_{p,q+1} - z_{p,q}) \tag{11.12}$$

![](img/66c45bbed85bb7ba7f7b05dff49b5060_284_0.png)

Figure 11.19. Left: This figure shows the depth of points at (p,q), (p,q+1), and (p+1,q) given by z_{p,q}, z_{p+1,q} and z_{p,q+1} respectively. The normal N = (N_x, N_y, N_z) recovered by the photometric stereo is shown as well. Right: This figure shows the assumptions on the light and camera set up for photometric stereo given by three or more non-coplanar lights and camera distant to the surface.

Note that since V_1 and V_2 are both perpendicular to N. Therefore, we can find two constraints, first of which is as follows.

```
0 = N · V_1  (11.13)
  = (N_x, N_y, N_z) · (1, 0, z_{p+1,q} - z_{p,q})  (11.14)
  = N_x + N_z(z_{p+1,q} - z_{p,q})  (11.15)
```

Similarly, the second constraint is given by

```
0 = N · V_2  (11.16)
  = (N_x, N_y, N_z) · (0, 1, z_{p,q+1} - z_{p,q})  (11.17)
  = N_y + N_z(z_{p,q+1} - z_{p,q})  (11.18)
```

There the two constraints can be summarized as

```
N_x / N_z = z_{p,q} - z_{p+1,q}  (11.19)
N_y / N_z = z_{p,q} - z_{p,q+1}  (11.20)
```

where the depth values are the only unknown.

Every pixel thus contributes to constraints involving the depths of its neighboring pixels. Considering the camera image of P × Q size, let us assume that

![](img/66c45bbed85bb7ba7f7b05dff49b5060_285_0.png)

Figure 11.20. From left: One of the input images; the recovered surface normals encoded by a RGB vector; the surface albedo; the reconstructed depth where depth is inversely proportional to the gray value; the same object relighted from a different virtual direction.

the total number of all such constraints is C. The value of C would have been 2PQ but for the pixels in the boundary for whom only one such constraint can be designed. Therefore, C < 2PQ but still sufficiently larger than PQ to create an over-constrained system of equations given by

M Z = B
(11.21)

where M is a C × PQ matrix whose entries can be either 1 or −1, Z is a PQ × 1 column vector containing the unknown depth and B is a same sized column vector of known scalar values. Therefore, Z can now be solved using a linear regression or singular value decomposition. The reconstructed depth is shown in Figure 11.18.

There are a few things to note from the above equations. We need to solve for three unknowns. Therefore, we need at least three lights (i.e. n = 3) to find the shape of the object. However, if the light directions are coplanar, L is rank-deficient and hence cannot be solved. Hence, we need at least three non-coplanar light directions. Other assumptions include that the camera image plane is parallel to the XY plane in the global coordinate system and the camera and the lights are distant from the object. Figure 11.19 shows that photometric stereo can give accurate surface normals but the recovered depth is inaccurate if the camera or the lights are placed very close to the object. Note that we do not need to find any correspondence unlike most stereo methods we have studied in Chapter 8 since the camera location does not change. Before processing the images in photometric stereo you have to undo the effect of the camera transfer function. Finally, once the surface normals and reflectance are computed, the object can be relighted from a light direction that was not available originally, as shown in Figure 11.20

![](img/66c45bbed85bb7ba7f7b05dff49b5060_286_0.png)

Figure 11.21. This figure shows the specular highlight on the chrome sphere in the scene when lighted from four different light directions.

![](img/66c45bbed85bb7ba7f7b05dff49b5060_286_1.png)

Figure 11.22. This figure shows the results of photometric stereo on color images in the presence of shadows. On the left we see the input images and on the right the reconstructed face geometry is shown from different views.

## 11.3.1 Handling Shadows

One limitation of photometric stereo stems from the shadows. If any pixel (p, q) is in shadow in the image i, its importance should be undermined. To achieve a formulation where such confidence can be imparted to the accuracy of the recorded illumination, we can weight each equation in Equation 11.8 by the pixel intensity recorded. The pixels in shadow will therefore be given less weight due to their lower intensity. This gives us the equations

```
\begin{pmatrix} I_1 \\ I_2 \\ . \\ . \\ . \\ I_n \end{pmatrix} - \rho \begin{pmatrix} I_1 L_1^x & I_1 L_1^y & I_1 L_1^z \\ I_2 L_2^x & I_2 L_2^y & I_2 L_2^z \\ \cdots \\ \cdots \\ \cdots \\ I_n L_n^x & I_n L_n^y & I_n L_n^z \end{pmatrix} \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} = 0 \quad (11.22)
```

that can be solved as before for more accurate normals.

## 11.3.2 Computing Illumination Directions

Photometric stereo computes the light directions also in addition to the surface geometry. To achieve this easily, one option is to put a chrome sphere of known radius r in the scene. This sphere will show specular highlights at different places
