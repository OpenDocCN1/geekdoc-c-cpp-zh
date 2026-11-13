# 2. Double Alternative.

This structure has the form
If condition, then:
[Module A]
Else:
[Module B]
[End of If structure.]

The logic of this structure is pictured in Fig. 2.4(b). As indicated by the flow chart, if the condition holds, then Module A is executed; otherwise Module B is executed.

# 3. Multiple Alternatives.

This structure has the form
If condition(1), then:
[Module A1]
Else if condition(2), then:
[Module A2]
:
Else if condition(M), then:
[Module AM]
Else:
[Module B]
[End of If structure.]

The logic of this structure allows only one of the modules to be executed. Specifically, either the module which follows the first condition which holds is executed, or the module which follows the final Else statement is executed. In practice, there will rarely be more than three alternatives.

# Example 2.5

The solutions of the quadratic equation
$ax^2 + bx + c = 0$
where $a \neq 0$, are given by the quadratic formula

```
$x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$
```

The quantity $D = b^2 - 4ac$ is called the *discriminant* of the equation. If $D$ is negative, then there are no real solutions. If $D = 0$, then there is only one (double) real solution, $x = -b/2a$. If $D$ is positive, the formula gives the two distinct real solutions. The following algorithm finds the solutions of a quadratic equation.

```
Algorithm 2.2: (Quadratic Equation) This algorithm inputs the coefficients A, B, C of a quadratic equation and outputs the real solutions, if any.
Step 1. Read: A, B, C.
Step 2. Set D: = B^2 - 4AC.
Step 3. If D > 0, then:
(a) Set X1 := (-B + \sqrt{D} )/2A and
X2 := (-B - \sqrt{D} )/2A.
```