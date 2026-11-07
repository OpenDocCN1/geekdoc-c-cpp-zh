# Summary of Operator Precedence and Grouping

The following table shows the precedence and grouping of the operators introduced to this point. The operators are shown from top to bottom in decreasing order of precedence.

| Operators | Grouping | Type |
|---|---|---|
| `++` (postfix)   `--` (postfix) | right to left | postfix |
| `+`   `-`   `++` (prefix)   `--` (prefix)   `(type)` | right to left | unary |
| `*`   `/`   `%` | left to right | multiplicative |
| `+`   `-` | left to right | additive |
| `<`   `<=`   `>`   `>=` | left to right | relational |
| `==`   `!=` | left to right | equality |
| `&&` | left to right | logical AND |
| `||` | left to right | logical OR |
| `?:` | right to left | conditional |
| `=`   `+=`   `-= `   `*=`   `/=`   `%=` | right to left | assignment |
| `,` | left to right | comma |

# The _Bool Data Type

The C standard includes a boolean type—represented by the keyword `_Bool`—which can hold only the values 0 or 1. Recall that the value 0 in a condition is *false*, while any nonzero value is *true*. Assigning any nonzero value to a _Bool sets it to 1. The standard also includes the `<stdbool.h>` header, which defines `bool` as a shorthand for the type _Bool, and `true` and `false` as named representations of 1 and 0, respectively. During preprocessing, the identifiers bool, true and false are replaced with _Bool, 1 and 0, respectively.

# Self Check

1. *(Multiple Choice)* When the following `if` statement executes, which pair of variable values would cause `seniorFemales` to be incremented?

```
if (gender == 1 && age >= 65) {
    ++seniorFemales;
}
```

+   a) gender is 2 and age is 60.
+   b) gender is 2 and age is 73.
+   c) gender is 1 and age is 19.
+   d) gender is 1 and age is 65.

**Answer: d.**

2. *(Multiple Choice)* When the following `if` statement executes, which pair of variable values would not cause "Student grade is A" to print?