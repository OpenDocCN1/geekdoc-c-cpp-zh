+   10. Use the "dynamicMatrix" object in Section 3.14 and the short-memory approach to implement the alternating-direction Godunov scheme in Section 9.11 to solve the system of nonlinear PDEs.

+   11. Show that Newton’s iteration in Section 9.8 that solves an equation of the form

$$\mathcal{D}(u)=F$$

(where $F$ is a given function, $u$ is the unknown function, and $\mathcal{D}$ is a nonlinear differential operator) can be viewed as a generalization of Newton’s iteration in Section 9.16 that finds the root of a function. Indeed, $u$ can be viewed as the "root" for which

$$\mathcal{D}(u)-F=0.$$

Furthermore, for every function $v$, let $\mathcal{L}_v$ be the linearization of $\mathcal{D}$ at $v$. Then, along the guidelines in Section 9.16, Newton’s iteration takes the form

$$u^{(i+1)}=u^{(i)}-\mathcal{L}_{u^{(i)}}^{-1}\left(\mathcal{D}(u^{(i)})-F\right)=u^{(i)}-\left(u^{(i)}-\mathcal{L}_{u^{(i)}}^{-1}F\right)=\mathcal{L}_{u^{(i)}}^{-1}F,$$

which is precisely the Newton iteration as described in Section 9.8.