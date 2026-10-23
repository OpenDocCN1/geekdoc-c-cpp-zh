```
x(i) += residual/d(i,i,"read");
}
return x;
}  // solving d*x=f approximately by 100 GS iterations
```

# 7.13 Two Spatial Dimensions

We turn now to the more complicated case of the convection-diffusion equation in two spatial dimensions (the Cartesian dimensions x and y). This equation has the form

$$u_t(t,x,y)-\varepsilon\left(u_{xx}(t,x,y)+u_{yy}(t,x,y)\right)$$
$$+C_1(t,x,y)u_x(t,x,y)+C_2(t,x,y)u_y(t,x,y)$$
$$=F(t,x,y),\quad 0<t<T,\ 0<x<L_x,\ 0<y<L_y,$$

where $T$, $L_x$, and $L_y$ are positive numbers denoting (respectively) the length of the time interval and the width and length of the two-dimensional spatial domain, and $C_1$ and $C_2$ are the given convection coefficients. In order to have a well-posed problem, initial and boundary conditions must also be imposed:

$$u(0,x,y)=u^{(0)}(x,y),\quad 0\le x\le L_x,\ 0\le y\le L_y,$$
$$u(t,x,L_y)=G(t,x,L_y),\quad 0\le t\le T,\ 0\le x\le L_x,$$
$$u(t,L_x,y)=G(t,L_x,y),\quad 0\le t\le T,\ 0\le y\le L_y,$$
$$\alpha(t,x,0)u(t,x,0)+u_n(t,x,0)=G(t,x,0),\quad 0\le t\le T,\ 0\le x\le L_x,$$
$$\alpha(t,0,y)u(t,0,y)+u_n(t,0,y)=G(t,0,y),\quad 0\le t\le T,\ 0\le y\le L_y.$$

where $F$, $G$, and $\alpha$ are given functions and $n$ is the outer normal vector; that is, $n=-x$ at $y=0$ and $n=-y$ at $x=0$. Thus, Dirichlet boundary conditions are imposed at the right and upper edges of the rectangular spatial domain, and mixed boundary conditions are imposed on the other two edges.

The finite-difference discretization is as in Section 7.3 above, except that here both the $x$- and $y$-derivatives should be discretized. Note also that here the spatial grid is rectangular as in Figure 7.4 rather than one-dimensional as in Section 7.3.

Let us now describe the finite-difference scheme in some more detail. Let $N_x$ and $N_y$ denote the number of grid points in the $x$ and $y$ spatial directions, respectively. Let $h_x=L_x/N_x$ and $h_y=L_y/N_y$ be the corresponding meshsizes. Then, the rectangular $N_x\times N_y$ grid that approximates the spatial domain is the set of pairs

$$(0,h_x,2h_x,\ldots,(N_x-1)h_x)\times(0,h_y,2h_y,\ldots,(N_y-1)h_y)$$