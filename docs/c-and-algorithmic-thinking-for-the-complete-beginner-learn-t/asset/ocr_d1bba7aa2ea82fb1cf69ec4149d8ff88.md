Let’s say that there is a region in memory, named **A** and it contains the number **13**.

![](bbox=[0.136, 0.09, 0.811, 0.316])

When a program instructs the CPU to execute the statement

```
A ← A + 1
```

the following procedure is executed:

+   - the number 13 is transferred from the RAM’s region named **A** to the CPU;
+   - the CPU calculates the sum of 13 and 1; and
+   - the result, 14, is transferred from the CPU to the RAM’s region named **A**, replacing the existing number, 13.

After execution, the RAM looks like this.

![](bbox=[0.341, 0.535, 0.591, 0.677])

# ### 7.2 Arithmetic Operators

Just like every high-level programming language, C++ supports almost all types of arithmetic operators.

| Arithmetic Operator | Description |
|---|---|
| + | Addition |
| - | Subtraction |
| * | Multiplication |
| / | Division |
| % | Modulus (remainder after integer division) |

The first four operators are straightforward and need no further explanation.