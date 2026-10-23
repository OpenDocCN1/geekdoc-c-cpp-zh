Furthermore, thanks to the fact that $\widetilde{N}_e$ is orthogonal, we also have

$$(S_t\widetilde{N}_e)^{-1}=\widetilde{N}_e^{-1}S_t^{-1}=\widetilde{N}_eS_t^{-1}.$$

Using also our default choice, we have the matrix equation

$$(S_t\widetilde{N}_e)^{-1}\begin{pmatrix}D_t(e^{(2)})-D_t(e^{(1)}) & 1 & 0 \\ 0 & 0 & 1 \\ 0 & 0 & 0\end{pmatrix}=\begin{pmatrix}0\\0\\\alpha\end{pmatrix}\,Y_{t,e}=\begin{pmatrix}0 & \widehat{Y}_{t,e}\\0 & \beta\\\alpha & \gamma\end{pmatrix}.$$

Using also our default assumption that $D_t(e)$ is not parallel to the $x$-$y$ plane, or that

$$\left(D_t(e^{(2)})-D_t(e^{(1)})\right)_3\neq 0,$$

we have that the left-hand side in the above matrix equation is a triple product of three nonsingular matrices. As a consequence, the matrix in the right-hand side is nonsingular as well, which implies that $\widehat{Y}_{t,e}$ is nonsingular as well, as asserted.

Using the above result, we can now define the edge-midpoint functions in $t$ by

$$\begin{pmatrix}R_{i,t}\\R_{i+1,t}\end{pmatrix}=\widehat{Y}_{t,e}^{-1}\begin{pmatrix}r_{i,t}\\r_{i+1,t}\end{pmatrix}.$$

For any polynomial of three variables $p(x,y,z)$ defined in $t$, let $p^{(i,t)}$ and $p^{(i+1,t)}$ denote its degrees of freedom at $D_t(w)$, or its directional derivatives (in the directions specified by the columns of the $3\times 2$ matrix $S_t\widetilde{N}_eY_{t,e}$) at $D_t(w)$. With our default choice, in particular, we have

$$p^{(i,t)}=p_x(D_t(w)),\\p^{(i+1,t)}=p_y(D_t(w)).$$

Let us verify that for the edge-midpoint functions defined above, these degrees of freedom are indeed as required:

$$R_{i,t}^{(i,t)}=R_{i+1,t}^{(i+1,t)}=1$$

and

$$R_{i,t}^{(i+1,t)}=R_{i+1,t}^{(i,t)}=0.$$

Indeed,

$$\begin{pmatrix}\nabla^tR_{i,t}\\\nabla^tR_{i+1,t}\end{pmatrix}S_t\widetilde{N}_eY_{t,e}=\widehat{Y}_{t,e}^{-1}\begin{pmatrix}\nabla^tr_{i,t}\\\nabla^tr_{i+1,t}\end{pmatrix}S_t\widetilde{N}_eY_{t,e}$$
$$=\widehat{Y}_{t,e}^{-1}\begin{pmatrix}(\nabla^tp_i)\circ D_t^{-1}\\(\nabla^tp_{i+1})\circ D_t^{-1}\end{pmatrix}S_t^{-1}S_t\widetilde{N}_eY_{t,e}$$
$$=\widehat{Y}_{t,e}^{-1}\left(\begin{pmatrix}(\nabla^tp_i)\circ D_t^{-1}\\(\nabla^tp_{i+1})\circ D_t^{-1}\end{pmatrix}\widetilde{N}_e\right)Y_{t,e}.$$