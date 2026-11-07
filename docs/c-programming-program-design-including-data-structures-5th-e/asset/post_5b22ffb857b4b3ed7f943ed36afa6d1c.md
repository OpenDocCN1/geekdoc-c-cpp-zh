
### EXAMPLE 4-1

| Expression | Meaning | Value |
|---|---|---|
| `8 < 15` | 8 is less than 15 | `true` |
| `6 != 6` | 6 is not equal to 6 | `false` |
| `2.5 > 5.8` | 2.5 is greater than 5.8 | `false` |
| `5.9 <= 7.5` | 5.9 is less than or equal to 7.5 | `true` |

## Comparing Characters

For char values, whether an expression using relational operators evaluates to true or false depends on a machine’s collating sequence. The collating sequence of some of the characters is:

| ASCII Value | Char | ASCII Value | Char | ASCII Value | Char | ASCII Value | Char |
|---:|:---:|---:|:---:|---:|:---:|---:|:---:|
| 32 | `' '` | 61 | `=` | 81 | `Q` | 105 | `i` |
| 33 | `!` | 62 | `>` | 82 | `R` | 106 | `j` |
| 34 | `"` | 65 | `A` | 83 | `S` | 107 | `k` |
| 42 | `*` | 66 | `B` | 84 | `T` | 108 | `l` |
| 43 | `+` | 67 | `C` | 85 | `U` | 109 | `m` |
| 45 | `-` | 68 | `D` | 86 | `V` | 110 | `n` |
| 47 | `/` | 69 | `E` | 87 | `W` | 111 | `o` |
| 48 | `0` | 70 | `F` | 88 | `X` | 112 | `p` |
| 49 | `1` | 71 | `G` | 89 | `Y` | 113 | `q` |
| 50 | `2` | 72 | `H` | 90 | `Z` | 114 | `r` |
| 51 | `3` | 73 | `I` | 97 | `a` | 115 | `s` |
| 52 | `4` | 74 | `J` | 98 | `b` | 116 | `t` |
| 53 | `5` | 75 | `K` | 99 | `c` | 117 | `u` |
| 54 | `6` | 76 | `L` | 100 | `d` | 118 | `v` |
| 55 | `7` | 77 | `M` | 101 | `e` | 119 | `w` |
| 56 | `8` | 78 | `N` | 102 | `f` | 120 | `x` |
| 57 | `9` | 79 | `O` | 103 | `g` | 121 | `y` |
| 60 | `<` | 80 | `P` | 104 | `h` | 122 | `z` |

The ASCII character set is described in Appendix C.

Now, because 32 < 97, and the ASCII value of ' ' is 32 and the ASCII value of 'a' is 97, it follows that ' ' < 'a' is true. Similarly, using the previous ASCII values:

```
`'R' > 'r'` is `false`
```

```
`'+' < '*'` is `false`
```

```
`'A' <= 'a'` is `true`
```

Note that comparing values of different data types may produce unpredictable results. For example, the following expression compares an integer and a character:

```
8 < '5'
```

In this expression, on a particular machine, 8 would be compared with the collating sequence of '5', which is 53. That is, 8 is compared with 53, which makes this particular expression evaluate to true.

Expressions such as `4 < 6` and `'R' > 'T'` are examples of **logical (Boolean) expressions**. When C++ evaluates a logical expression, it returns an integer value of 1 if the logical expression evaluates to true; it returns an integer value of 0 otherwise. In C++, any nonzero value is treated as true.

> **NOTE.** Chapter 2 introduced the data type `bool`. Recall that the data type bool has two values, `true` and `false`. In C++, `true` and `false` are reserved words. The identifier `true` is set to 1, and the identifier `false` is set to 0. For readability, whenever logical expressions are used, the identifiers `true` and `false` will be used here as the value of the logical expression.

## Relational Operators and the `string` Type

The relational operators can be applied to variables of type string. Variables of type string are compared character by character, starting with the first character and using the ASCII collating sequence. The character-by-character comparison continues until either a mismatch is found or the last characters have been compared and are equal. The following example shows how variables of type string are compared.

### EXAMPLE 4-2

Suppose that you have the statements:

```
string str1 = "Hello";
string str2 = "Hi";
string str3 = "Air";
string str4 = "Bill";
string str5 = "Big";
```

The following expressions show how string relational expressions evaluate.

| Expression | Value/Explanation |
|---|---|
| `str1 < str2` | **true**<br>`str1 = "Hello"` and `str2 = "Hi"`. The first characters of `str1` and `str2` are the same, but the second character `'e'` of `str1` is less than the second character `'i'` of `str2`. Therefore, `str1 < str2` is true. |
| `str1 > "Hen"` | false<br>`str1 = "Hello"`. The first two characters of `str1` and `"Hen"` are the same, but the third character `'l'` of `str1` is less than the third character `'n'` of `"Hen"`. Therefore, `str1 > "Hen"` is false. |
| `str3 < "An"` | true<br>`str3 = "Air"`. The first characters of `str3` and `"An"` are the same, but the second character `'i'` of `"Air"` is less than the second character `'n'` of `"An"`. Therefore, `str3 < "An"` is true. |
| `str1 == "hello"` | false<br>`str1 = "Hello"`. The first character `'H'` of `str1` is less than the first character `'h'` of `"hello"` because the ASCII value of `'H'` is 72, and the ASCII value of `'h'` is 104. Therefore, `str1 == "hello"` is false. |
| `str3 <= str4` | true<br>`str3 = "Air"` and `str4 = "Bill"`. The first character `'A'` of `str3` is less than the first character `'B'` of `str4`. Therefore, `str3 <= str4` is true. |
| `str2 > str4` | true<br>`str2 = "Hi"` and `str4 = "Bill"`. The first character `'H'` of `str2` is greater than the first character `'B'` of `str4`. Therefore, `str2 > str4` is true. |

If two strings of different lengths are compared and the character-by-character comparison is equal until it reaches the last character of the shorter string, the shorter string is evaluated as less than the larger string, as shown next.

| Expression | Value/Explanation |
|---|---|
| `str4 >= "Billy"` | false<br>`str4 = "Bill"`. It has four characters, and `"Billy"` has five characters. Therefore, `str4` is the shorter string. All four characters of `str4` are the same as the corresponding first four characters of `"Billy"`, and `"Billy"` is the larger string. Therefore, `str4 >= "Billy"` is false. |
| `str5 <= "Bigger"` | true<br>`str5 = "Big"`. It has three characters, and `"Bigger"` has six characters. Therefore, `str5` is the shorter string. All three characters of `str5` are the same as the corresponding first three characters of `"Bigger"`, and `"Bigger"` is the larger string. Therefore, `str5 <= "Bigger"` is true. |

The program Chapter4_StringComparisons.cpp at the Web site accompanying this book shows the results of the previous expressions.

## Logical (Boolean) Operators and Logical Expressions

This section describes how to form and evaluate logical expressions that are combinations of other logical expressions. **Logical (Boolean) operators** enable you to combine logical expressions. C++ has three logical (Boolean) operators, as shown in Table 4-2.

**TABLE 4-2** Logical (Boolean) Operators in C++

| Operator | Description |
| --- | --- |
| `!` | not |
| `&&` | and |
| `\|\|` | or |

Logical operators take only logical values as operands and yield only logical values as results. The operator ! is unary, so it has only one operand. The operators && and || are binary operators. Tables 4-3, 4-4, and 4-5 define these operators.

Table 4-3 defines the operator ! (not). When you use the ! operator, !true is false and !false is true. Putting ! in front of a logical expression reverses the value of that logical expression.

**TABLE 4-3** The ! (Not) Operator

| Expression | !(Expression) |
| --- | --- |
| `true (nonzero)` | `false (0)` |
| `false (0)` | `true (1)` |

### EXAMPLE 4-3

| Expression | Value | Explanation |
| --- | --- | --- |
| `!('A' > 'B')` | true | Because `'A' > 'B'` is false, `!('A' > 'B')` is true. |
| `!(6 <= 7)` | false | Because `6 <= 7` is true, `!(6 <= 7)` is false. |

Table 4-4 defines the operator `&&` (and). From this table, it follows that `Expression1 && Expression2` is true if and only if both `Expression1` and `Expression2` are true; otherwise, `Expression1 && Expression2` evaluates to `false`.

**TABLE 4-4** The `&&` (And) Operator

| Expression1 | Expression2 | Expression1 && Expression2 |
|---|---|---|
| `true` (nonzero) | `true` (nonzero) | `true` (1) |
| `true` (nonzero) | `false` (0) | `false` (0) |
| `false` (0) | `true` (nonzero) | `false` (0) |
| `false` (0) | `false` (0) | `false` (0) |

### EXAMPLE 4-4

| Expression | Value | Explanation |
|---|---|---|
| `(14 >= 5) && ('A' < 'B')` | `true` | Because `(14 >= 5)` is `true`, `('A' < 'B')` is `true`, and `true && true` is `true`, the expression evaluates to `true`. |
| `(24 >= 35) && ('A' < 'B')` | `false` | Because `(24 >= 35)` is `false`, `('A' < 'B')` is `true`, and `false && true` is `false`, the expression evaluates to `false`. |

Table 4-5 defines the operator `||` (or). From this table, it follows that `Expression1 || Expression2` is true if and only if at least one of the expressions, `Expression1` or `Expression2`, is true; otherwise, `Expression1 || Expression2` evaluates to `false`.

**TABLE 4-5** The `||` (Or) Operator

| Expression1 | Expression2 | Expression1 \|\| Expression2 |
|---|---|---|
| `true` (nonzero) | `true` (nonzero) | `true` (1) |
| `true` (nonzero) | `false` (0) | `true` (1) |
| `false` (0) | `true` (nonzero) | `true` (1) |
| `false` (0) | `false` (0) | `false` (0) |

![](img/f97f778697507bb6fdd80c5991210cba_224_0.png)
