# Iteration 2

Now compute ∇g(x₁) = (32.719, −14.645). We move from (2.785, 4.988) in the direction of (32.719, −14.645). How far do we go along the line L(t) = (2.785, 4.988) + (32.719, −14.645)t? We need to maximize the function

$$g(L(t)) = g(x_1 + t \cdot \nabla g(x_1))$$

$$= 322.33 + 1285.0t - 7499.3t^2.$$

This function can also be maximized by simple single-variable calculus:

$$\frac{d}{dt}g(L(t)) = 0 \quad\Longrightarrow\quad t^* = 0.08567$$

The new point x₂ is found by evaluating L(t*) = x₁ + t* · ∇g(x₁).

$$x_2 = (5.588, 3.733)$$

Since ‖x₂ − x₁‖ > 0.01, we must iterate again.

Use our *SteepestAscent* function to have Maple finish the iterations. Define g as a function of the vector x.

```
g := x → −4x₁² − 15x₂² + 55x₁ + 135x₂ − 100:
```