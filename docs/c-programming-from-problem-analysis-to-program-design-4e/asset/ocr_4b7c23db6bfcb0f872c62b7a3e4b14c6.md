```
answer = x * y;    // Here x and y are both operands.
examScore greater than 89    // examScore and 89 are operands.
finalGrade is equal to 'A'   // finalGrade and 'A' are operands.
```

To construct a conditional expression, after you identify the operands, determine what type of comparison to make. In Example 5-1, pseudocode demonstrated how to compare a variable against a value. However, to write those statements in C#, you use special symbols to represent the operations. The next section describes the types of operators that can be used.

# Equality, Relational, and Logical Tests

You can use equality, relational, and logical operators in conditional expressions. To determine whether two values are the same, use the equality operator.

# EQUALITY OPERATORS

Two equal symbol characters == are used as the equality operator in C# for comparing operands. No space is inserted between the symbols. Recall that the single equal symbol (=), called the assignment operator, is used to assign the result of an expression to a variable. You cannot use the assignment operator in a selection statement in C#.

> > **NOTE**
> > Languages such as Java and C++ allow you to use a single equal symbol inside a conditional expression. This often creates an error that takes time to find. Failing to put two equal symbols in a conditional expression leads to an assignment being made. The side effect of this is that the expression always evaluates to true, unless the assignment statement assigns zero to a variable. You never have this problem in C# because C# issues a syntax error if you use the assignment operator in a location where the equality operator is expected.

An exclamation point followed by a single equal symbol (!=) represents NOT equal. As with the equality operator, no space is embedded between the exclamation point and equal symbol. Table 5-1 shows examples of the use of equality operators.

TABLE 5-1 Equality operators

| Symbol | Meaning | Example | Result |
|---|---|---|---|
| == | Equal | (1 == 2) | false |
| != | NOT equal | (4 != (19 % 5)) | false |