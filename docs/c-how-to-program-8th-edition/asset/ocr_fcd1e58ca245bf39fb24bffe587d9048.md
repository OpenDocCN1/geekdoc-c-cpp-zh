Figure 6.31 shows how function fibonacci would evaluate `fibonacci(3)`. This figure raises some interesting issues about the order in which C++ compilers evaluate the operands of operators. This is a separate issue from the order in which operators are applied to their operands, namely, the order dictated by the rules of operator precedence and associativity. Figure 6.31 shows that evaluating `fibonacci(3)` causes two recursive calls, namely, `fibonacci(2)` and `fibonacci(1)`. In what order are these calls made?

![](bbox=[0.143, 0.232, 0.856, 0.504])

**Fig. 6.31**  |  Set of recursive calls to function `fibonacci`.

# *Order of Evaluation of Operands*

Most programmers simply assume that the operands are evaluated left to right. C++ does not specify the order in which the operands of most operators (including `+`) are to be evaluated. Therefore, you must make no assumption about the order in which these calls execute. The calls could in fact execute `fibonacci(2)` first, then `fibonacci(1)`, or they could execute in the reverse order: `fibonacci(1)`, then `fibonacci(2)`. In this program and in most others, it turns out that the final result would be the same. However, in some programs the evaluation of an operand can have side effects (changes to data values) that could affect the final result of the expression.

C++ specifies the order of evaluation of the operands of only four operators—`&&`, `||`, comma (`,`), and `?:`. The first three are binary operators whose two operands are guaranteed to be evaluated left to right. The last operator is C++’s only ternary operator—its leftmost operand is always evaluated first; if it evaluates to nonzero (`true`), the middle operand evaluates next and the last operand is ignored; if the leftmost operand evaluates to zero (`false`), the third operand evaluates next and the middle operand is ignored.

> **Portability Tip 6.2**
> 
> Programs that depend on the order of evaluation of the operands of operators other than `&&`, `||`, and the comma (`,`) operator can function differently with different compilers.

> **Common Programming Error 6.14**
> 
> Writing programs that depend on the order of evaluation of the operands of operators other than `&&`, `||`, and the comma (`,`) operator can lead to logic errors.