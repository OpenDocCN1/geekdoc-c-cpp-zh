Many modern languages provide facilities that prevent this kind of error from happening in the first place. For example, C++ uses short-circuit evaluation: if the first operand of the and is false, the second isn’t evaluated because the whole expression would be false anyway. In other words, in C++ the only part of

```
if ( SomethingFalse && SomeCondition ) ...
```

that’s evaluated is SomethingFalse. Evaluation stops as soon as SomethingFalse is identified as false.

Evaluation is similarly short-circuited with the or operator. In C++ and Java, the only part of

```
if ( somethingTrue || someCondition ) ...
```

that is evaluated is somethingTrue. The evaluation stops as soon as somethingTrue is identified as true because the expression is always true if any part of it is true. As a result of this method of evaluation, the following statement is a fine, legal statement.

# Java Example of a Test That Works Because of Short-Circuit Evaluation

```
if ( ( denominator != 0 ) && ( ( item / denominator ) > MIN_VALUE ) ) ...
```

If this full expression were evaluated when denominator equaled 0, the division in the second operand would produce a divide-by-zero error. But since the second part isn’t evaluated unless the first part is true, it is never evaluated when denominator equals 0, so no divide-by-zero error occurs.

On the other hand, because the && (and) is evaluated left to right, the following logically equivalent statement doesn’t work:

# Java Example of a Test That Short-Circuit Evaluation Doesn’t Rescue

```
if ( ( ( item / denominator ) > MIN_VALUE ) && ( denominator != 0 ) ) ...
```

In this case, item / denominator is evaluated before denominator != 0. Consequently, this code commits the divide-by-zero error.

Java further complicates this picture by providing “logical” operators. Java’s logical & and | operators guarantee that all terms will be fully evaluated regardless of whether the truth or falsity of the expression could be determined without a full evaluation. In other words, in Java, this is safe:

# Java Example of a Test That Works Because of Short-Circuit (Conditional) Evaluation

```
if ( ( denominator != 0 ) && ( ( item / denominator ) > MIN_VALUE ) ) ...
```