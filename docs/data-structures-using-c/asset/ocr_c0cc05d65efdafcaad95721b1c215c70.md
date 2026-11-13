An expression in one form can be converted to the other two forms. Let us write algorithms for all these conversions.

+   1. Infix expression to postfix expression
+   2. Infix expression to prefix expression
+   3. Prefix expression to infix expression
+   4. Prefix expression to postfix expression
+   5. Postfix expression to infix expression
+   6. Postfix expression to prefix expression

Let E be the expression made of characters. Characters here include operators, operands, and delimiters. In addition, let '#' be the character denoting the end of the expression.

# Infix to Postfix Conversion

Algorithm 3.2 illustrates the infix to postfix conversion.

# ALGORITHM 3.2

```
1. Scan expression E from left to right, character by character, till character is '#'
   ch = get_next_token(E)
2. while(ch != '#')
   if(ch == ')') then ch = pop()
   while(ch != '(')
   Display ch
   ch = pop()
   end while
   if(ch == operand) display the same
   if(ch == operator) then
   if(ICP > ISP) then push(ch)
   else
   while(ICP <= ISP)
   pop the operator and display it
   end while
   ch = get_next_token(E)
   end while
3. if(ch == '#') then while(!emptystack()) pop and display
4. stop
```

For this algorithm, we refer to the operators and the respective ICPs and ISPs as assigned in Table 3.8. Example 3.2 illustrates the conversion of an infix expression to its postfix form (function in Program Code 3.5).

# EXAMPLE 3.2

Convert the following infix expression to its postfix form:

A ^ B × C – C + D|A(E + F)

# Solution

Conversion of infix to postfix form can be illustrated as in Table 3.9