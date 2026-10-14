Expanding this, we get the following equation at each pixel $(p,q)$ for each light $L_i$.

$$R_i - \rho \begin{pmatrix} L_i^x & L_i^y & L_i^z \end{pmatrix} \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} = 0 \tag{11.7}$$

Taking into account all the $n$ lights we get

$$\begin{pmatrix} R_1 \\ R_2 \\ . \\ . \\ R_n \end{pmatrix} - \rho \begin{pmatrix} L_1^x & L_1^y & L_1^z \\ L_2^x & L_2^y & L_2^z \\ \cdots \\ \cdots \\ L_n^x & L_n^y & L_n^z \end{pmatrix} \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} = 0 \tag{11.8}$$

Rearranging the terms, we get

$$\begin{pmatrix} L_1^x & L_1^y & L_1^z \\ L_2^x & L_2^y & L_2^z \\ \cdots \\ \cdots \\ \cdots \\ L_n^x & L_n^y & L_n^z \end{pmatrix}^{-1} \begin{pmatrix} R_1 \\ R_2 \\ . \\ . \\ . \\ R_n \end{pmatrix} = \rho \begin{pmatrix} N_x \\ N_y \\ N_z \end{pmatrix} \tag{11.9}$$

$$\text{or } \mathbf{L}^{-1}\mathbf{R} = \rho N \tag{11.10}$$

where $\mathbf{L}^{-1}$ is the pseudo-inverse of the non-square matrix $L$. Note that, at every pixel $(p,q)$ the light directions and the intensity recorded are known. Each term in the left hand side of the Equation 11.10 is known. Therefore, we compute the right hand side of the equation and the vector obtained is the normal vector at the point on the object scaled by $\rho$. The magnitude of this vector provide reflectance $\rho$ at $(p,q)$ and the corresponding unit vector provide the normal $N$. This is illustrated in Figure 11.18.

The above process gives us the surface normal at any pixel $(p,q)$ and its reflectance, but not its depth. So, in the next step we need to find the depth of the surface with respect to the camera. Let us consider the camera’s coordinate system and the surface as shown in Figure 11.19. Let the depth of points at $(p,q)$, $(p,q+1)$, and $(p+1,q)$ given by $z_{p,q}$, $z_{p+1,q}$ and $z_{p,q+1}$ respectively. Note that the tangent plane to the normal $N = (N_x, N_y, N_y)$ recovered by the photometric stereo can be approximated by the vectors $V_1$ and $V_2$, assuming a smoothly varying normal, and is given by

$$V_1 = (p+1, q, z_{p+1,q}) - (p, q, z_{p,q}) = (1, 0, z_{p+1,q} - z_{p,q}) \tag{11.11}$$

$$V_2 = (p, q+1, z_{p,q+1}) - (p, q, z_{p,q}) = (0, 1, z_{p,q+1} - z_{p,q}) \tag{11.12}$$