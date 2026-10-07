# Appendix D Operator Precedence

Some symbols, such as * and &, are used for more than one operator. In such cases, one form is unary (one operand), and the other is binary (two operands), and the compiler uses the context to determine which is meant.Table D.1 labels operator groups unary or binary cases in which the same symbol is used for two ways.

The following are some examples of precedence and associativity.
Here's an example in which the compiler has to decide whether to add 5 to 3 or multiply 5 by 6:

```
3 + 5 * 6
```

The * operator has higher precedence than the + operator, so it is applied to the 5 first, making the expression 3 + 30, or 33.
Here's an example in which the compiler has to decide whether to divide 6 into 120 or multiply 6 by 5:

```
120 / 6 * 5
```

Both / * have the same precedence, but these operators associate from left to right. That means the operator to the left of the shared operand (6) is applied first, so the expression becomes 20 * 5, or 100.
Here's an example in which the compiler has to decide whether to begin by incrementing str or dereferencing str:

```
char * str = "Woa";
char ch = *str++;
```

The ++ operator has higher precedence than the unary * operator. This means the increment operator operates on str and not *str.That is, the operation increments the pointer, making it point to the next character, rather than altering after the character pointed to. However, because *str is the post form, the pointer is incremented after the value of *str is assigned to ch.Therefore, this expression assigns the w to ch and moves str to point to the h character.
Here's a similar example:

```
char * str = "Woa";
char ch = ++str;
```

The ++ operator and the unary * operator have the same precedence, but associate right-to-left. So, again, str and not *str is incremented. Because the ++ operator is in prefix form, first str is incremented and then the result is dereferenced. Thus, str moves to point to the h character, and the h character is assigned to ch.
Note that Table D.1 uses binary or unary in the “Precedence” column to distinguish between two operators that use the same symbol, such as the unary address operator and the binarywise AND operator.

Appendix B,"C++ Reserved words,”lists alternative representations for some of the operators.