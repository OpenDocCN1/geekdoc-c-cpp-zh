value of either Constraint 1 or Constraint 2, the objective value will increase by approximately −λ · Δ = Δ. The geometric interpretation reinforces the computational results, giving them meaning and fully showing the effect of binding constraints (constraints where μ_i^2 = 0) on the solution.

The following is a short Maple session of the computations above.

```
with(Student[MultivariateCalculus]);
f := (x, y) → 3x + 2y:
Constrnt := [2x + y − 100, x + y − 80]:
L := (x, y, λ₁, λ₂, μ₁, μ₂) → f(x, y) + λ₁·Constrnt[1] + λ₂·Constrnt[2] + μ₁² + μ₂²:
grad := Gradient(L(x, y, λ₁, λ₂, μ₁, μ₂), [x, y, λ₁, λ₂, μ₁, μ₂]):
NecCond := [seq(G = 0, G in grad)]:
(NecCond);
```

```
3 + 2λ₁ + λ₂ = 0
2 + λ₁ + λ₂ = 0
μ₁² + 2x + y − 100 = 0
μ₂² + x + y − 80 = 0
2λ₁μ₁ = 0
2λ₂μ₂ = 0
```

```
soln := solve(NecCond, [x, y, λ₁, λ₂, μ₁, μ₂]);
soln := [[x = 20, y = 60, λ₁ = −1, λ₂ = −1, μ₁ = 0, μ₂ = 0]];
f(20, 60);
subs(x = 20, y = 60, Constraint);
180
[0, 0]
```

How do we know we’ve found a maximum? Recall the rules for finding the maximum or minimum.

MAXIMUM: If f(x) is a concave function and each constraint gᵢ(x) is a convex function, then any point that satisfies the necessary conditions is an optimal solution that maximizes the function subject to the constraints and has each λᵢ ≤ 0.

MINIMUM: If f(x) is a convex function and each constraint gᵢ(x) is a convex function, then any point that satisfies the necessary conditions is an optimal solution that minimizes the function subject to the constraints and has each λᵢ > 0.

The objective function is linear, and so is both convex and concave, as are the constraints. Since the values of λᵢ are both negative, we have found the maximum.

We can use Maple’s own LagrangeMultipliers.

```
LagrangeMultipliers(f(x, y), Constrnt, [x, y], output = detailed);
[x = 20, y = 60, λ₁ = 1, λ₂ = 1.3 · x + 2 · y = 180]
```

Note the sign difference on Maple’s λs. Explain how this occurs.