by the term

```
(Δt/2)√(1+u²_{i,j}) F(iΔt, jh)
```

if the value u_{i+1/2,j+1/2} in Section 9.4 is the same as u_{i,j} or

```
(Δt/2)√(1+u²_{i,j+1}) F(iΔt, (j+1)h)
```

if the value u_{i+1/2,j+1/2} in Section 9.4 is the same as u_{i,j+1}. The above approximation to the integral of F(t,x(t)) along the characteristic line x(t) that leads to ((i+1/2)Δt,(j+1/2)h) (see Figure 9.9) should then be added to the value of u_{i+1/2,j+1/2} in Section 9.4 to produce the correct value in the inhomogeneous case. This completes the definition of the modified Godunov scheme in the inhomogeneous case.

In the next section, we use the above modification to extend the Godunov scheme to the vector conservation law.

# 9.11 System of Nonlinear PDEs

Here, we consider the extension of the singularly perturbed Riemann problem in Section 9.7 to the case of two spatial dimensions x and y and two unknown functions u(t,x,y) and v(t,x,y), which are coupled in the following system of nonlinear PDEs:

```
-ε(u_{xx}(t,x,y)+u_{yy}(t,x,y))+u_t(t,x,y)
+u(t,x,y)u_x(t,x,y)+v(t,x,y)u_y(t,x,y)
=F_1(t,x,y),
-ε(v_{xx}(t,x,y)+v_{yy}(t,x,y))+v_t(t,x,y)
+u(t,x,y)v_x(t,x,y)+v(t,x,y)v_y(t,x,y)
=F_2(t,x,y).
```

where F_1(t,x,y) and F_2(t,x,y) are given functions, and x and y are the independent variables in a two-dimensional domain, with suitable initial and boundary conditions. The above system of PDEs is also called a system of singularly perturbed conservation laws.

The characteristic lines for this system are defined in the three-dimensional (t,x,y) space. In fact, they are defined by the vector (t,x(t),y(t)) satisfying

```
dx(t)/dt = u(t,x(t),y(t)) and dy(t)/dt = v(t,x(t),y(t)).
```

With this definition, we have from the chain rule that, when ε = 0,

```
du(t,x(t),y(t))/dt = u_t(t,x(t),y(t))+u(t,x(t),y(t))u_x(t,x(t),y(t))
+ v(t,x(t),y(t))u_y(t,x(t),y(t))
= F_1(t,x(t),y(t)),
 dv(t,x(t),y(t))/dt = v_t(t,x(t),y(t))+u(t,x(t),y(t))v_x(t,x(t),y(t))
+ v(t,x(t),y(t))v_y(t,x(t),y(t))
= F_2(t,x(t),y(t)).
```

Thus, the initial and boundary conditions about u and v travel along the characteristic lines (or curves) to form the solution in the entire time-space domain.