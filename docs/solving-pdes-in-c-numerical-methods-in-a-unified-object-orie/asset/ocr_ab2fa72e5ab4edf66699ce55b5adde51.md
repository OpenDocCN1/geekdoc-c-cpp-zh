# Chapter 21

# The Stokes Equations

In this chapter, we present the Stokes equations and their relation to the general linear elasticity equations. The present adaptive-refinement algorithm uses modified multigrid to solve linear elasticity problems that approximate the original Stokes equation. On the finest mesh, a Schur-complement preconditioner is used to solve the original Stokes equations. Other algorithms to solve the Stokes and Navier–Stokes equations are also described.

# 21.1 The Nabla Operator

In order to present the Stokes and Navier–Stokes equations that model fluid dynamics, we need the Nabla operator, denoted by ∇. This operator acts differently on scalar and vector functions. Furthermore, its interpretation depends on the arithmetic symbol that follows it.

The Nabla operator acts upon scalar and vector functions of three spatial variables x, y, and z. For example, let’s consider the scalar function

```
s ≡ s(x, y, z)
```

and the vector function

```
v ≡ (v₁(x, y, z), v₂(x, y, z), v₃(x, y, z)).
```

In what follows, we assume that the scalar functions s, v₁, v₂, and v₃ are differentiable to the second order; that is, they have well-defined second derivatives, including mixed ones.

The Nabla operator may be interpreted in three different ways. The interpretation depends on the symbol that follows the ∇ symbol and the type of function that follows it.

When the ∇ symbol is followed by the name of a function with no arithmetic symbol in between, it is interpreted as the gradient operator:

```
∇ = ( ∂/∂x 
      ∂/∂y 
      ∂/∂z )
```