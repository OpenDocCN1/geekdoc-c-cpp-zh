The value stored in `charges` would be 175. The first expression (`timeAtSite < 2.0`) evaluates to `false`; thus, the last expression (`timeAtSite * 50.00`) is evaluated and 175 is stored in `charges`.

![](bbox=[0.175, 0.18, 0.237, 0.233])

The ternary conditional operator is not as readable as the `if` statement. The `if` statement is used more often than other forms of the selection statement.

# Order of Operations

When an expression contains multiple operators, the **precedence of the operators** controls the order in which the individual operators are evaluated. For example, you saw in Chapter 2 that an expression such as `value1 + value2 * value3` is evaluated as `value1 + (value2 * value3)` because the `*` operator has higher precedence than the `+` operator.

Generally speaking, the precedence of operators follows the following order:

+   1. Unary operators
+   2. Binary operators
+      1. Arithmetic operators (`* / %` in front of `+ -`)
+      2. Relational operators (`<< >>` in front of `== !=`)
+      3. Logical operators (`&&` in front of `||`)
+   3. Ternary operator (`? :`)
+   4. Assignment operators (`=, *= /= %= += -=`)

In Table 3–1, the operators used primarily for arithmetic were presented. Table 5–7 adds the operators presented in this chapter.