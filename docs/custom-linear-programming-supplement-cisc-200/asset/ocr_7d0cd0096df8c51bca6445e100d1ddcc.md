Because 5 tons of material 2 are available for production, the mathematical statement of constraint 2 is

```
0.2S ≤ 5
```

# Constraint 3:

Tons of material 3 used ≤ Tons of material 3 available

Every ton of fuel additive RMC produces will use 0.6 tons of material 3. Thus, 0.6F tons of material 1 is used to produce F tons of fuel additive. Similarly, every ton of solvent base RMC produces will use 0.3 tons of material 3. Thus, 0.3S tons of material 1 is used to produce S tons of solvent base. Therefore, the number of tons of material 3 used to produce F tons of fuel additive and S tons of solvent base is

```
Tons of material 3 used = 0.6F + 0.3S
```

Because 21 tons of material 3 are available for production, the mathematical statement of constraint 3 is

```
0.6F + 0.3S ≤ 21
```

# Add the Nonnegativity Constraints

RMC cannot produce a negative number of tons of fuel additive or a negative number of tons of solvent base. Therefore, nonnegativity constraints must be added to prevent the decision variables F and S from having negative values. These nonnegativity constraints are

```
F ≥ 0 and S ≥ 0
```

Nonnegativity constraints are a general feature of many linear programming problems and may be written in the abbreviated form:

```
F, S ≥ 0
```

# Mathematical Model for the RMC Problem

Problem formulation is now complete. We have succeeded in translating the verbal statement of the RMC problem into the following mathematical model:

```
Max 40F + 30S
Subject to (s.t.)
0.4F + 0.55S ≤ 20 Material 1
0.2S ≤ 5 Material 2
0.6F + 0.3S ≤ 21 Material 3
F, S ≥ 0
```

Our job now is to find the product mix (i.e., the combination of F and S) that satisfies all the constraints and, at the same time, yields a maximum value for the objective function. Once these values of F and S are calculated, we will have found the optimal solution to the problem. This mathematical model of the RMC problem is a linear program. The RMC problem has an objective and constraints that, as we said earlier, are common properties of all