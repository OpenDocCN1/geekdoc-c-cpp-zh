# 27.1 Rotation Mode Algorithm

The CORDIC methods are based on iteratively rotating a point by fixed angles until a desired rotation is achieved. The equations for rotating a point (x,y) about the origin in two dimensions are

```
x' = xcosθ - ysinθ
y' = xsinθ + ycosθ,
```

and these are equivalent to

```
x' = cosθ(x - ytanθ)
y' = cosθ(y + xtanθ).
```

The main concept behind the CORDIC methods is to iteratively rotate the point by angles whose tangent is a power of two until the desired angle is reached using the formula

```
x_{i+1} = C_i(x_i - d_i y_i 2^{-i})
y_{i+1} = C_i(y_i + d_i x_i 2^{-i}),
```

where

```
C_i = cos(tan^{-1} 2^{-i}) = \frac{1}{\sqrt{1 + 2^{-2i}}}.
```

Choosing a power of two allows the multiplication by tanθ to be replaced with a shift operation.

Because the values of C_i are constant, the multiplication by C_i in each iteration can be moved out of the iteration process, and the