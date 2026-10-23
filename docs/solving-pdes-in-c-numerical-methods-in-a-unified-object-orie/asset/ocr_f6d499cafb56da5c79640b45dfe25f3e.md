# 27.5 The Nonlinear Term

The coefficient |u|² in the nonlinear term K₁|u|²u in the Helmholtz equation is nondifferentiable so long as it is considered as a standard complex-valued function. To make it differentiable (and, hence, ready for the Newton iteration of Section 9.14), its real part must be separated from its imaginary part.

Consider a complex-valued grid function v, defined on the nodes in the mesh M. Note that v may be viewed as a vector, whose i-th component, v_i, is the same as the returned value v(i). Furthermore, v can be written in terms of its real and imaginary parts:

```
v_i = Re v_i + sqrt(-1) Im v_i.
```

(Such a separation is used in [4] to apply a finite-difference scheme to the one-dimensional nonlinear Helmholtz equation.) Furthermore, the complex number v_i can be interpreted as a point in the two-dimensional Cartesian plane:

```
v_i = ( Re v_i \ Im v_i ) .
```

In this interpretation, v can be viewed as a function from the nodes in M to the Cartesian plane. This is why the function v is also called below a vector grid function.

Consider now an operator f that transforms the complex-valued grid function v into another complex-valued grid function f(v). In fact, f(v) can also be written in terms of its real and imaginary parts:

```
f(v)_i = Re f(v)_i + sqrt(-1) Im f(v)_i,   i ∈ M.
```

Furthermore, f(v)_i can also be interpreted as a point in the two-dimensional Cartesian plane:

```
f(v)_i = ( Re f(v)_i \ Im f(v)_i ) .
```

This way, f(v) is interpreted as a vector grid function as well, and f is actually interpreted as an operator on the set of vector grid functions.

To define the operator f more specifically, let us first introduce a helpful notation. For every tetrahedron

```
t = (k, l, m, n) ∈ M,
```

let us denote the polynomial of three variables

```
P_t(v) ≡ v_k P_{k,t} + v_l P_{l,t} + v_m P_{m,t} + v_n P_{n,t}.
```

As above, this polynomial can also be written in terms of its real and imaginary parts:

```
P_t(v) = Re P_t(v) + sqrt(-1) Im P_t(v)
= Re v_k P_{k,t} + Re v_l P_{l,t} + Re v_m P_{m,t} + Re v_n P_{n,t}
+ sqrt(-1) ( Im v_k P_{k,t} + Im v_l P_{l,t} + Im v_m P_{m,t} + Im v_n P_{n,t} ).
```