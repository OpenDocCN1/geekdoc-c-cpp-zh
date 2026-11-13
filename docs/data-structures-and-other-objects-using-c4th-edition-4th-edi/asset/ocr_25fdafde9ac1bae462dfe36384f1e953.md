+   1. The operands are in the right order

Let's consider each of these four issues. First we need to know that the operands (the numbers and variables) in the postfix expression are in the same order as they were in the input infix expression, but this is easy to see. Because operands are written out as soon as they are read in, they are clearly in the same order as in the input infix expression.

+   2. The parentheses are done correctly

Parentheses are a way of grouping subexpressions. Everything inside a pair of matching parentheses is treated as a single unit by anything outside the parentheses. The parentheses give the following message to the operations outside of the parentheses: Don't look inside these parentheses. We will work things out among ourselves and deliver a single value for you to combine with other operands. This means that all operations between a set of matching parentheses in the infix expression should form a subexpression of the postfix expression, and with this algorithm they do just that. To see that they do form a subexpression, we will show the following:

# How the Infix-to-Postfix Algorithm Translates Subexpressions

Claim: All of the operations between a pair of matching parentheses (and no other operations) are output between the time the algorithm reads the opening parenthesis and the time that it reads the closing parenthesis.

Once we show that this claim is true, we will know that all the operations between a pair of matching parentheses in the infix expression will be together in a group within the output postfix notation, and so they will form a subexpression of the postfix expression. So, let's see exactly why the claim is valid.

The algorithm keeps track of expressions within matching parentheses by using its stack. When the algorithm encounters an opening parenthesis, that is, a '(', it pushes this parenthesis onto the stack. Now consider what happens between pushing the opening parenthesis and encountering the matching closing parenthesis, that is, the matching ')'. The algorithm will never output an operation from the stack that is below the opening parenthesis, '('. Thus, it only outputs operations that are within the pair of matching parentheses in the input (infix) expression. Moreover, it outputs all of these operations. When it encounters the matching closing parenthesis, it outputs all the remaining operations on the stack all the way down to that matching opening parenthesis.

+   3. The precedence is handled correctly

When the infix expression contains an operation with low precedence followed by an operator with a higher precedence, then the algorithm should output these operations in reverse order. In other words, the higher precedence operation must be written first. A check of the algorithm will show that the operations are indeed output in reverse order.