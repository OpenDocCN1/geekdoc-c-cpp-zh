second-order accurate. One possibility is the box scheme (see Duffy, 2006, p. 110) which is essentially one-step averaging in space and time:

```
- \frac{B_{j+1/2}^{n+1} - B_{j+1/2}^{n}}{\Delta t} + \alpha \frac{B_{j+1}^{n+1/2} - B_{j}^{n+1/2}}{h} = 0
```

where:

```
B_{j+1/2}^{n} \equiv \frac{1}{2}(B_{j+1}^{n} + B_{j}^{n}), \quad B_{j}^{n+1/2} \equiv \frac{1}{2}(B_{j}^{n+1} + B_{j}^{n}).
```

+   f) Create a mini-ADE scheme near y = 0 by solving for B_0^{n+1} and B_1^{n+1} and then apply the standard ADE method from the second mesh point in space.
+   g) Compare the accuracy of all ADE schemes and their variations with the exact solution.

# 3. (ADE for Two-Dimensional Problems Project)

In the interests of completeness, we discuss the applicability of ADE to n-factor PDEs. To this end, we consider the two-dimensional heat equation with a given inhomogeneous forcing term f(x, y, t) and Dirichlet boundary conditions g(x, y) on the unit square:

```
\frac{\partial u}{\partial t} = \frac{\partial^2 u}{\partial x^2} + \frac{\partial^2 u}{\partial y^2} + f(x, y, t) \text{ in } (0,1)^2 \times (0,T)

u(x,y,0) = g(x,y) \text{ on the boundary of } (0,1)^2.
```

Answer the following questions:

+   a) In the case of the heat equation in the quarter plane (0, ∞) × (0, ∞) use a domain transformation defined by:
+   
+   z = \frac{x}{x + \alpha_1}, w = \frac{y}{y + \alpha_2}
+   
+   In this case α₁ and α₂ are user-defined parameters.
+   What is the new PDE in the coordinates z and w?

+   b) We consider a two-dimensional mesh and corresponding discrete mesh functions indexed by indices i and j in the directions x and y, respectively. A straightforward generalisation of the Barakat–Clark method to two dimensions is:

```
\frac{U_{i,j}^{n+1} - U_{i,j}^{n}}{k} = \frac{1}{h_1^2}\left(U_{i-1,j}^{m+1} - U_{i,j}^{m+1} - U_{i,j}^{n} + U_{i+1,j}^{n}\right) + \frac{1}{h_2^2}\left(U_{i,j-1}^{n+1} - U_{i,j}^{n+1} - U_{i,j}^{n} + U_{i,j+1}^{n}\right),
```

```
\frac{V_{i,j}^{n+1} - V_{i,j}^{n}}{k} = \frac{1}{h_1^2}\left(V_{i-1,j}^{n} - V_{i,j}^{n} - V_{i,j}^{n+1} + V_{i+1,j}^{n+1}\right) + \frac{1}{h_2^2}\left(V_{i,j-1}^{n} - V_{i,j}^{n} + V_{i,j}^{n+1} + V_{i,j+1}^{n+1}\right),
```

```
u_{i,j}^{n} = \frac{1}{2}\left(U_{i,j}^{n} + V_{i,j}^{n}\right).
```

This scheme consists of two ‘sweeps’; the first sweep uses boundary conditions starting at corner (0, 0) while the second sweep uses boundary conditions starting at corner (1, 1). See Figure 21.3.