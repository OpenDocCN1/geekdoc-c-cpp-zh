7 Nil A b a *+dc/

8 Nil nil empty empty dc/ba*+

The final prefix output that we get is dc/ba*+ whose reverse is +*ab/cd, which is the prefix equivalent of the input infix expression a*b+c*d. Note that all the operands are simply pushed to the queue in steps 1, 3, 5, and 7. In step 2, the operator / is pushed to the empty stack of operators.

In step 4, the operator + is checked against the elements in the stack. Since / (division) has higher priority than + (addition), the queue is emptied to the prefix output (thus we get ‘dc’ as the output) and then the operator / is written (thus we get ‘dc/’ as the output). The operator + is then pushed to the stack. In step 6, the operator * is checked against the stack elements. Since * (multiplication) has a higher priority than + (addition), * is pushed to the stack. Step 8 signifies that all of the infix expression is scanned. Thus, the queue of operands is emptied to the prefix output (to get ‘dc/ba’), followed by the emptying of the stack of operators (to get ‘dc/ba*+’).

# Points to remember

+   1. A prefix expression is parenthesis-free.
+   2. To convert an infix expression to the prefix equivalent, it is scanned from right to left. The prefix expression we get is the reverse of the required prefix equivalent.
+   3. Conversion of infix to prefix requires a queue of operands and a stack, as in the conversion of an infix to postfix.
+   4. The order of operands in a prefix expression is the same as that in its infix equivalent.
+   5. If the scanned operator o1 and the operator o2 at the stack top have the same priority, then the associativity of o2 is checked. If o2 is rightassociative, it is popped from the stack.

# Self Assessment Questions:

3. Stack is also called _____ data structure.