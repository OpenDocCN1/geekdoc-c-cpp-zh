# 11.12.5 Nullable Boolean & and | operators

The nullable Boolean type `bool?` can represent three values, true, false, and null.

As with the other binary operators, lifted forms of the logical operators & and | (§11.12.4) are also pre-defined:

```
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

The semantics of the lifted & and | operators are defined by the following table:

| x | y | x & y | x | y |
|---|---|---|---|---|
| true | true | true | true |
| true | false | false | true |
| true | null | null | true |
| false | true | false | true |
| false | false | false | false |
| false | null | false | null |
| null | true | null | true |
| null | false | false | null |
| null | null | null | null |

Note: The bool? type is conceptually similar to the three-valued type used for Boolean expressions in SQL. The table above follows the same semantics as SQL, whereas applying the rules of §11.4.8 to the & and | operators would not. The rules of §11.4.8 already provide SQL-like semantics for the lifted ^ operator. end note

# 11.13 Conditional logical operators

# 11.13.1 General

The && and || operators are called the conditional logical operators. They are also called the "short-circuiting" logical operators.

```
conditional_and_expression
  : inclusive_or_expression
  | conditional_and_expression '&&' inclusive_or_expression
  ;

conditional_or_expression
  : conditional_and_expression
  | conditional_or_expression '||' conditional_and_expression
  ;
```

The && and || operators are conditional versions of the & and | operators:

+   - The operation x && y corresponds to the operation x & y, except that y is evaluated only if x is not false.
+   - The operation x || y corresponds to the operation x | y, except that y is evaluated only if x is not true.