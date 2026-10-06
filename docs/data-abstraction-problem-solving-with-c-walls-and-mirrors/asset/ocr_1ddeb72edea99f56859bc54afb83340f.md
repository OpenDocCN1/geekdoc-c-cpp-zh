# 208 CHAPTER 6 Stacks

requires a more complex algorithm. The following is a high-level description of what you must do when you encounter each character as you read the infix string from left to right

Five steps in the process to convert from infix to postfix

+   1. When you encounter an operand, append it to the output string postfixExp.
Justification: The order of the operands in the postfix expression is the same as the order in the infix expression, and the operators that appear to the left of an operator in the infix expression also appear to its left in the postfix expression.
2. Push "+\ onto the stack.
3. When you encounter an operator, push it onto the stack. However, if the stack is not empty, pop operators of greater or equal precedence from the stack and append them until you encounter either a "+\ or an operator of lower precedence or the stack becomes empty. You then push the current operator onto the stack. This step orders the operators by precedence and in accordance with left-to-right association. Notice that you continue popping from the stack until you encounter an operator of strictly lower precedence than the current operator in the infix expression. You do not stop on equality, the left-to-right association rule says that in case of a tie in precedence, the leftmost operator is applied first—and this operator that is the one at last.
4. When you encounter a "(", pop operators off the stack and append to the end of postfixExp until you encounter the matching "".
Justification: Within a pair of parentheses, precedence and left-to-right association determine the order of the operators, and step 3 has ordered the operators with these rules.
5. When you reach the end of the string, push the remaining contents of the stack to postfixExp.

For example, 6-5 traces the action of the algorithm on the infix expression $a-(b+c*d)/e$, assuming that the stack A and postfixExp are initially empty. Then the algorithm contains the resulting postfix expression $a b c d*+ e/-

You can use the previous five-step description of the algorithm to develop a fairly concise pseudocode solution, which follows. The symbol $ullet$ in this algorithm means concatenate(join,)

# FIGURE 6-5 A trace of the algorithm that converts the infix expression $a-(b+c*d)/e$ to postfix form

| aStack (bottom to top) | postfixExp |
|---|---|
| a | a |
| | a |
| ( | a |
| ( - ( | a |
| b - ( | ab |
| + - + | abc |
| c - + | abc |
| * - + * | abcd Move operators from stack to |
| d - + * | abcd postfixExp until "*" |
| ) - + | abcd++ |
| - | abcd++ |
| / - / | abcd++ |
| - - / | Copy operators from |
| e - / | stack to postfixExp |
| | abcd+ e/- |