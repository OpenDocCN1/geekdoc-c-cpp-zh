(b) y = --b;

![](bbox=[0.06, 0.076, 0.47, 0.15])

To clarify, suppose that an int variable a has the value 5. Consider the assignment

```
b = ++a;
```

Pre-increment implies

+   - Step 1: increment a;        /* a becomes 6 */
+   - Step 2: assign this value to b; /* b becomes 6 */
+   - Result: a is 6, b is 6

If it is a 'post' operator, the value of the operand is altered after it is fetched for computation. The unaltered value is used in the computation of the expression in which it occurs. Suppose again that a has the value 5 and consider the assignment

```
b = a++;
```

Post-increment implies

+   - Step 1: assign the unincremented a to b; /* b becomes 5 */
+   - Step 2: increment a; /* a becomes 6 */
+   - Result: a is 6, b is 5

The placement of the operator before or after the operand directly affects the value of the operand that is used in the computation. When the operator is positioned before the operand, the value of the operand is altered before it is used. When the operator is placed after the operand, the value of the operand is changed after it is used. Note in the examples above that the variable a has been incremented in each case.

Suppose that the int variable n has the value 5. Now consider a statement such as

```
x = n++ / 2;
```

The post-increment operator, possessing a higher priority than all other operators in the statement, is evaluated first. But the value of n that is used in the computation of x is still 5. Post-increment implies using the current value of n in the computation and incrementing it immediately afterwards.

So x gets the value 5/2 = 2, even though n becomes 6. The rule is repeated; in an expression in which a post-incremented or post-decremented operand occurs, the current (unaltered) value of the operand is used; only then, is it changed. Accordingly, in the present instance, 5 is the value of n that is used in the computation. n itself becomes 6.

Now, consider the following statement.

```
x = ++n / 2;
```

where n is initially 5.

Pre-increment or pre-decrement first alters the operand n; it is this new value that is used in the evaluation of x. In the example, n becomes 6, as before; but this new value is used in the computation, not 5. So x gets the value 6/2 = 3.

Now, consider the following program:

```
int main()
{
    int x=5;
    printf("Values are %d and %d\n",x++,++x);
    return 0;
}
```

Before revealing the results, let us see if we can work out what the output of the program will be. Here, it is needed to consider the values passed to the printf() function. The first part of the expression is “x++”. This is a post-increment(use-and-increment) expression, so the value of the expression is 5 and as a side effect of evaluating the expression the value of x is increased to 6. Next, the value of the expression “++x” is calculated. This is the pre-increment (increment-and-use) expression, so the value of the expression is clearly 7. Thus the expected output is

Values are 5 and 7

Some compilers give this expected output but trying the same program using the Turbo C as well as GCC based compiler for example in Quincy 2005 resulted in the output

Values are 6 and 7

This is rather surprising but it can easily be explained. The C programming language standard rules quite specifically allow the parameters to be passed to a function to be evaluated in any convenient order. Some compilers worked left to right, which seems more natural, whereas others worked right to left which may be more efficient in some circumstances.

This must be remembered when writing programs that are to be compiled on many different machines. A similar difficulty arises when considering the output of a program such as

```
int main()
{
    int x = 4;
    printf("Result = %d\n",x++ + x);
    return 0;
}
```

Since the standard allows expressions involving commutative associative operators such as “+” to be evaluated in any order, a moment’s thought shows that the value printed out would be 8 for right-to-left evaluation and 9 for left-to-right evaluation. On the Quincy 2005, the output was