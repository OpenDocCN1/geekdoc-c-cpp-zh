
Algorithm 3.1 lists the steps involved in the evaluation of the postfix expression E.

```
ALGORITHM 3.1
1. Let E denote the postfix expression
2. Let Stack denote the stack data structure to be used and let Top = -1
3. while(1) do
   begin
   X = get_next_token(E) // Token is an operator, operand, or delimiter
   if(X = #) (end of expression)
   then return
   if(X is an operand)
   then push(X) onto Stack
   else X is operator)
   begin
   OP1 = pop() from Stack
   OP2 = pop() from Stack
   Tmp = evaluate(OP1, X, OP2)
   push(Tmp) on Stack
   end
   [If X is operator then pop the correct number of operands
   from stack for operator X. Perform the operation and push the
   result, if any, onto the stack.]
   end
4. stop
```

It is assumed that the last character in E is '#'. A procedure get_next_token is used to extract the next token from E. A token is an operand, an operator, or a #. A one-dimensional array Stack[n] is used as a stack.

Let us consider an example postfix expression E = AB + C#. Now, let us scan this expression from left to right, character by character, as represented in Fig. 3.13.

This evaluation process is much simpler than the evaluation of the infix expression.

Let us now devise an algorithm for converting an infix expression to a postfix notation. To see how to devise an algorithm for translating from infix to postfix, note that the operands in both notations appear in the same sequence. Let us also learn how we can manually convert an infix expression into a postfix expression.

The following are the steps for manually converting an expression from one notation to another:

- 1. Initially, fully parenthesize the given infix expression. Use operator precedence and associativity rules for the same.
- 2. Now, move all operators so that they replace their corresponding right parenthesis.
- 3. Finally, delete all parentheses, and we get the postfix expression.

![](img/a99ec79093c067f0bed8f1086197950e_127_0.png)

## Fig. 3.13 Evaluation of postfix expression AB + C#

The evaluation of a postfix expression is simple, but now we need to convert an infix expression to its postfix form. Let us consider an example E = A/B ^ C + D x E - A x C.

Let us fully parenthesize the same as

E = (((A / B ^ C) + (D x E)) - (A x C))

Let us move all operators to the corresponding right parenthesis and replace the same.

E = (((A / B ^ C) + (D x E)) - (A x C))

Now let us eliminate all parentheses. We get the postfix equivalent of the infix expression.

E(postfix) = ABC ^ / DE x + AC x -

This method can be used to get an equivalent prefix notation too as follows:

(((A / B ^ C) + (D x E)) - (A x C))

We now get the prefix expression after eliminating the parentheses as

```
E(prefix) = -/+ A ^ BC / DE x AC
```

This procedure is a suitable method to manually convert the expression only. Let us try to work out the algorithm to convert an infix to a postfix (also to prefix).

We have observed that the order of the operand remains the same in the infix and the postfix notations. The output of the conversion should be a postfix notation. This postfix expression has a sequence of operands which is the same as that of the input infix expression. Hence, the operands from the infix expression can be immediately sent to the output as they occur. To handle the operators, the operands are stored in the stack until the right moment and they are unstacked (removed from the stack); they are then passed to the output.

For example, Let E be an infix expression as

```
E = A + B x C
```

After conversion, the expression should yield ABCx+, that is, the sequence of stacking them should be as given in Table 3.3.

## Table 3.3 Infix to postfix conversion of the expression E = A + B x C

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| + | + | A |
| B | + | AB |

Now, we have to decide about the operator x. This is illustrated in Table 3.4(a).

Here, note that the algorithm must decide whether the operator x gets placed on the top of the stack or the operator + is to be popped off. Since operator x has the highest priority, we should stack it so as to get the sequence of operations for expression X2 as shown in Table 3.4(b).

## Table 3.4 Handling and stacking of the x operator in expressions

### (a) Handling of the x operator

| | Infix | Postfix |
|---|---|---|
| Examples | X1 = (A + B) x C | AB + C x |
| | X2 = A + (B x C) | ABC x + |

## Table 3.4 (Continued)

### (b) Stacking of the × operator

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| + | + | A |
| B | + | AB |
| × | +× | AB |
| C | +× | ABC |
| # (Pop all) | +× | ABC ×+ |

In addition, when the input is exhausted, we should output all remaining operators in the stack to get the postfix expression as ABC×+.

Let us consider one more example. The infix expression A × (B + C) × D, after conversion, should generate the postfix expression ABC + × D ×, and hence, the sequence of operations should be as shown in Table 3.5.

## Table 3.5 Infix to postfix conversion of the expression A × (B + C) × D

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| × | × | A |
| ( | ×( | A |
| B | ×( | AB |
| + | ×(+ | AB |
| C | ×(+ | ABC |

(Continued)

At this point, unstack the corresponding left parenthesis and then delete the left and right parentheses; this should give the stack contents as follows:

## Table 3.5 (Continued)

| Next character | Stack | Output |
|---|---|---|
| ) | × | ABC+ |
| × | × | ABC+× |
| D | × | ABC+× D |
| Done | Empty | ABC+× D× |

From these examples and discussion, we can say that the operators are popped out of the stack if their in-stack priority (ISP) is greater than the priority of the incoming operator that is to be added onto the stack.

Consider the infix expression E = A x B + C#. The conversion of this expression into its postfix form is shown in Table 3.6.

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| x | x | A |
| B | x | AB |
| + | x + | ABx |
| C | + | AB x C |
| # (Pop all) | + | AB x C+ |

Now, let us consider the infix expression X = A ^ B ^ C

For its equivalent postfix expression, the sequence of push and pop operations should be as given in Table 3.7.

| Next character | Stack | Output |
|---|---|---|
| A | Empty | A |
| ^ | ^ | A |
| B | ^ | AB |
| ^ | ^ | |

We have decided the strategy for pushing and popping out the operator from the stack. In this example, the operator at the top of the stack and the operator to be pushed onto the stack are the same. If this rule is applied, then the input is AB ^ C ^, which is wrong! Hence, we need to add a few more checks. We must take into account the associativity of operators and prepare a hierarchy scheme for the binary arithmetic operators and delimiters. When an operator is at the top of the stack or in an expression (current token), they are to be treated with different priorities, as shown in Table 3.8.

| Symbol | In-stack priority (ISP) | Incoming priority (ICP) |
|---|---|---|
| ) | - | - |
| ^ | 3 | 4 |
| */ | 2 | 2 |
| +- | 1 | 1 |
| ( | 0 | 4 |

Thus, we can say that when the operators are taken out from the stack, their ISP is greater than or equal to the ICP of the new operator.

Hence, each operator is to be assigned two priorities—the incoming priority (ICP) and the in-stack priority (ISP). Incoming priority is considered when the operator is located in the given infix expression, whereas ISP is the priority when the operator is at the top of the stack. In Example 3.1, we observed that the lower priority operators should spend more time in the stack and the higher priority operators should be popped out earlier. To achieve this, we need to assign the appropriate ICPs and ISPs to the operators. Table 3.8 shows these values. If the incoming operator is the same as that of the in-stack operator and if the operator is left associative, then the operator from the stack should be popped and printed.

For example, consider the infix expressions X = A × B × C and Y = A/B × C. The expression X = A × B × C should yield the postfix expression as AB × C ×, and Y = A/B × C should generate the postfix expression as AB/C×.

If the priority of the operator on the top of stack (in-stack operator) is greater than the priority of the operator coming from the expression (incoming operator), then incoming operator is pushed onto the stack.

In short, the following points should be taken into consideration while assigning ICPs and ISPs:

- 1. Higher priority operators should be assigned higher values of ISP and ICP.
- 2. For right associative operators, ISP should be lower than ICP. For example, A ^ B ^ C should generate ABC^^, which means (A) ^ (B ^ C).
- 3. If ICP is higher than ISP, the operator should be stacked.
- 4. The ISP and ICP should be equal for left associative operators.

## Summing up

The following are the steps involved in the evaluation of an expression.

- 1. Assign priorities to all operators and define associativity (left or right).
- 2. Assign appropriate values of ICPs and ISPs accordingly. For left associative operators, assign equal ISP and ICP. For right associative operators, assign higher ICP than ISP. For example, assign a higher ICP for ‘^’ and for the right parenthesis ‘)’.
- 3. Scan the expression from left to right, character by character, till the end of expression.
- 4. If the character is an operand, then display the same.
- 5. If the character is an operator and if ICP > ISP then push the operator else while(ICP <= ISP) pop the operator and display it. end while Stack the incoming operator
- 6. Continue till end of expression

The expression could be in one of the three forms—infix, postfix, or prefix.
