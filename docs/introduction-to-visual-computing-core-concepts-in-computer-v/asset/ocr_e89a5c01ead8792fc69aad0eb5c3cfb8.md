have the same format where the last column will have the translation parameters. Therefore, we denote this with 𝒯(tₓ, tᵧ). Anytime we use this notation we will refer to a matrix where the top left sub-matrix is identity and the translation parameters go to the last column.

![](bbox=[0.17, 0.27, 0.35, 0.38])

Every transformation has an inverse. This is defined as the transformation that takes the transformed point P′ back to P. It is intuitive that the inverse of a translation would be another translation whose parameters are negated. Or, in other words,

```
𝒯⁻¹(tₓ, tᵧ) = 𝒯(−tₓ, −tᵧ)    (6.6)
```

This is consistent with the math, since x = x′ − tₓ and y = y′ − tᵧ. We can extend this to 3D as

```
𝒯(tₓ, tᵧ, t_z) = ⎛ 1 0 0 tₓ ⎞
                 ⎜ 0 1 0 tᵧ ⎟
                 ⎜ 0 0 1 t_z ⎟
                 ⎝ 0 0 0 1   ⎠    (6.7)
```

```
and
𝒯⁻¹ = 𝒯(−tₓ, tᵧ, −t_z)    (6.8)
```

You can verify this by finding the inverse of 𝒯 using standard matrix algebra.

Figure 6.3. This shows a point (x, y) being rotated by an angle θ to be transformed to the point (x′, y′).

# 6.3.2 Rotation

Next, we will consider the case of another Euclidean transformation, the rotation. Here also we will first consider the easier case of 2D rotation. For this, please take a look at Figure 6.3. This shows a point P = (x, y) being rotated by an angle θ to be transformed to the point P′ = (x′, y′).

Consider the point P in polar coordinates given by the length r and angle φ. P is then expressed as

```
x = r cos(φ)    (6.9)
y = r sin(φ)    (6.10)
```

The rotation can be expressed using the equations

```
x′ = r cos(θ + φ)    (6.11)
    = r cos(θ) cos(φ) − r sin(θ) sin(φ)    (6.12)
    = x cos(θ) − y sin(θ)    (6.13)
y′ = r sin(θ + φ)    (6.14)
    = r sin(θ) cos(φ) + r cos(θ) sin(φ)    (6.15)
    = x sin(θ) + y cos(θ)    (6.16)
```