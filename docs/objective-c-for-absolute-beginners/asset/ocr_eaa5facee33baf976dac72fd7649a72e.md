# CHAPTER 4: Making Decisions About...and Program Flow

Binary operators take two operands. Unary operators take one operand; AND and OR are binary operators, and NOT is a unary operator.

We just introduced a couple of new terms that can sound confusing; however, probably use Boolean logic every day. Let's look a couple of Boolean logic examples with the binary operators AND and OR in a conversation sometimes have with their teenage children.

"You can go to the movies tonight if your room is clean AND the dishes are put away."
"You can go to the movies tonight if your room is clean OR the dishes are put away"

Boolean operators' results are either TRUE or FALSE. In Chapter 3, we briefly introduced the Boolean data type. A variable that is defined as Boolean can only contain the values TRUE and FALSE.

```
BOOL seeMovies = FALSE;
```

In the preceding example, the AND operator takes two operands: one to the left and to the right of AND. Each operand can be evaluated independently with TRUE or FALSE.

For an AND operation to yield a TRUE result, both sides of the AND have to be TRUE. In our first example, the teenager has to clean his room AND the dishes are done. If either one of the conditions is FALSE, the result is FALSE–no movies for the teenager.

For an OR operation to yield a TRUE result, only one operand has to be TRUE, or both conditions can be TRUE to yield a TRUE result. In our second example, just a clean bedroom would result in the ability to go to the movies.

> NOTE: Behind the scenes, your iPhone/iPad/Mac defines a FALSE as a 0 and a TRUE as a 1. To be technically correct, a TRUE is defined as any non-zero value; so, values of 0.1, 1, and 2 would be evaluated as TRUE when evaluated in Boolean expression.

A NOT statement is a unary operator. It takes one operand to yield a Boolean result. Example:

"You cannot go to the movies."

This example takes one operand. The NOT operator turns a TRUE operand to a FALSE and a FALSE operand to a TRUE. Here, the result is FALSE.

> NOTE: Performing a NOT operation is commonly referred to as flipping-the-bit, or negating. TRUE is defined as a 1, FALSE is defined as a 0, and zeros and ones are referred to as bits. NOT operation turns a TRUE to a FALSE and a FALSE to a TRUE, hence flipping-the-bit or negating the result.

AND, OR, and NOT are three common Boolean operators. Occasionally, you will need to use more complex operators. XOR, NAND, and NOR are common operations for iPhone/iPad/Mac developers.