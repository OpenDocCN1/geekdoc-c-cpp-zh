The operators given in the following table are called **relational operators** because they test a relationship between two operands:

| Relational Operator | Relation Tested |
|---|---|
| `<` | Is less than |
| `>` | Is greater than |
| `==` | Is equal to |
| `!=` | Is not equal to |
| `<=` | Is less than or equal to |
| `>=` | Is greater than or equal to |

They are used in boolean expressions of the form

```
expression₁ relational_operator expression₂
```

where expression₁ and expression₂ have compatible types. For example, if root, a, b, and c are of type double, count is int, and answer is of type char, then the following are valid boolean expressions formed using these relational operators:

```
root < 1
b * b >= 4.0 * a * c
count == 100
answer != 'T'
```

If root has the value 0.7, then the expression

```
root < 1
```

has the value `true`. Similarly, if count has the value 99, then the expression

```
count == 100
```

produces the value `false`.

As illustrated by the expression answer != 'T', char values may also be compared using relational operators. As we saw in Chapter 3, characters are represented in memory by numeric codes, commonly ASCII (see Appendix A), and when two characters are compared, it is their numeric codes that are compared. For example, if char1 and char2 are character variables initialized by

```
char char1 = 'A', char2 = 'B';
```

the boolean expression

```
char1 < char2
```