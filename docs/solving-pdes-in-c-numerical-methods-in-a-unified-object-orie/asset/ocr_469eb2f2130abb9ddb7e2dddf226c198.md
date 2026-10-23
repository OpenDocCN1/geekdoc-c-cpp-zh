When the above Nabla operators are multiplied in the reverse order (gradient of divergence), we get the following 3 × 3 matrix of second derivatives:

```
∇∇· = (∂/∂x \ ∂/∂y \ ∂/∂z) (∂/∂x, ∂/∂y, ∂/∂z)
= ⎛ ∂²/∂x²   ∂²/∂x∂y   ∂²/∂x∂z ⎞
  ⎜ ∂²/∂y∂x   ∂²/∂y²   ∂²/∂y∂z ⎟
  ⎝ ∂²/∂z∂x   ∂²/∂z∂y   ∂²/∂z² ⎠
```

When the ∇ operator is followed by the × symbol, it then represents the curl or rotor operator. This operator can be represented by the 3 × 3 matrix

```
∇× = ⎛ 0      -∂/∂z   ∂/∂y ⎞
     ⎜ ∂/∂z   0      -∂/∂x ⎟
     ⎝ -∂/∂y  ∂/∂x   0    ⎠
```

This operator acts upon vector functions to produce their curl (rotor) vector functions:

```
∇×v = ⎛ 0      -∂/∂z   ∂/∂y ⎞ v
      ⎜ ∂/∂z   0      -∂/∂x ⎟
      ⎝ -∂/∂y  ∂/∂x   0    ⎠
= ⎛ v₃(x,y,z)ᵧ - v₂(x,y,z)ᶻ ⎞
  ⎜ v₁(x,y,z)ᶻ - v₃(x,y,z)ₓ ⎟
  ⎝ v₂(x,y,z)ₓ - v₁(x,y,z)ᵧ ⎠
```

If a vector function v satisfies

```
∇×v = 0
```

at every spatial point (x, y, z), then v is referred to as a conservative vector field. In this case, v has a scalar potential function Φ(x, y, z), of which v is the negative of the gradient, i.e.,

```
v = -∇Φ,
```

at every spatial point (x, y, z).

Conversely, if a vector function v has a scalar potential function φ, then it has zero curl:

```
∇×∇φ = 0,
```

where the 0 on the right stands for the zero three-dimensional vector. As a result, we also have

```
∇×∇v = 0,
```