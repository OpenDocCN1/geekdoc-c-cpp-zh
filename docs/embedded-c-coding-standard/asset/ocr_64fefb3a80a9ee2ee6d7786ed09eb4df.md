# 1.4 Parentheses

Rules:

+   - Do not rely on C’s operator precedence rules, as they may not be obvious to those who maintain the code. To clarity, use parentheses (and/or) break long statements into multiple lines of (code) to ensure proper execution order within a sequence of operations.

+   - Unless it is a single identifier or constant, each operand of the logical AND (&&) & logical OR (||) operators shall be surrounded by parentheses.

Example:

```
if ((depth_in_cm > 0) && (depth_in_cm < MAX_DEPTH))
{
depth_in_ft = convert_depth_to_ft(depth_in_cm);
}
```

Reasoning: The syntax of the C programming language has many operators. The precedence rules that dictate which operators are evaluated before which others are complicated—with over a dozen priority levels—and not always obvious to all programmers. When in doubt it’s better to be explicit about what you hope the compiler will do with your calculations.

Enforcement: These rules shall be enforced during code reviews.

![](bbox=[0.796, 0.166, 0.856, 0.219])