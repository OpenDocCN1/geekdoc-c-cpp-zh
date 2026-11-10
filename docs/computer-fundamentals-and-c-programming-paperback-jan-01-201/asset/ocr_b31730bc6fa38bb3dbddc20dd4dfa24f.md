# 6 Operators and Expressions

# WHAT TO LEARN

+   - Attributes of *operators* and their role in evaluating *expressions*.
+   - Significance of the *arithmetic* operators.
+   - How data types of variables and constants are *implicitly* changed.
+   - Role of *casts* in *explicit* conversion of data types.
+   - Using operator *precedence* and *associativity* in evaluating expressions.
+   - Significance of the *assignment* operators (`+=`, `-=`, `*=`, etc.).
+   - The increment (`++`) and decrement (`--`) operators and their *side effects*.
+   - Boolean evaluation of expressions using *relational* and *logical* operators.
+   - Use of the *conditional* and **sizeof** operators.

# 6.1 EXPRESSIONS

Variables and constants represent data in their most elemental form. These data objects become useful when combined with one another to form *expressions*. The components of an expression are linked to one another by symbols called *operators*. For instance, `a + b / 7` is an expression where `+` and `/` are operators. The expression has a *value* which here is evaluated arithmetically.

An arithmetic expression is not the only type of expression you’ll encounter in C. There are other types—like relational and logical expressions. For instance, `a > b` is not an arithmetic expression but it still has a value. The following examples illustrate the diversity of expressions used in C:

| C Construct | Expression | |
|---|---|---|
| `interest = principal * rate / 100;` | `principal * rate / 100` | *(arithmetic)* |
| `if (age > 18)` | `age > 18` | *(relational)* |
| `while (answer == 'y')` | `answer == 'y'` | *(relational)* |
| `if (age > 15 && age < 25)` | `age > 15 && age < 25` | *(logical)* |