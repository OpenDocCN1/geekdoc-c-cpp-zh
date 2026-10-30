```
```text
> opt := fsolve(NecessCond, {λ, x, y});
  opt := {λ = -0.7608695652, x = 1.673913043, y = 0.9782608696}
> subs(opt, L(x, y, λ)), subs(opt, f(x, y));
  10.44565217, 10.44565217
```
```

Explain why these two values are equal!

It will be no surprise that Maple has several commands for finding solutions to a constrained optimization problem; choose which command to use depending on the form of the output needed. Table 4.5 shows the most commonly used commands.

TABLE 4.5: Maple Commands for Constrained Optimization

| Package | Command |
|---|---|
| Student[MultivariateCalculus] | LagrangeMultipliers |
| *Basic Form:* `LagrangeMultipliers(ObjectiveFcn, [constraints], [vars], options)` | |
| *Options:* return more detailed report and/or plots | |
| Optimization | NLPSolve |
| *Basic Form:* `NLPSolve(ObjectiveFcn, [constraints], options)` | |
| *Options:* set solving method, starting point, detailed output, etc. | |
| Optimization | Maximize/Minimize |
| *Basic Form:* `Maximize(ObjectiveFcn, [constraints], options)`<br>`Minimize(ObjectiveFcn, [constraints], options)` | |
| *Options:* recommended: set a starting point | |

Remember, in “real world problems,” a critical element of the solution using the Lagrange multiplier method is the value and interpretation of the multiplier λ.

# Using Lagrange Multipliers

```
```text
> with(Student[MultivariateCalculus]):
> Obj := f(x, y)
  Obj := −2x² + xy − 2y² + 8x + 3y
> Cnstr := 3x + y − 6 :
```
```