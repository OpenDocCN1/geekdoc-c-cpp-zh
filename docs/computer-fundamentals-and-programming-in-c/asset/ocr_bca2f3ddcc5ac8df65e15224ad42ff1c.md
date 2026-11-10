Now, look at the output of this program. Could it be possible to predict the values a, b, and c? Never assume a variable to have a meaningful value, unless a value is assigned to it.

# ## Unary operators

The unary '-' operator negates the value of its operand (clearly, a signed number). A numeric constant is assumed positive unless it is preceded by the negative operator. That is, there is no unary '+'. It is implicit. Remember that -x does not change the value of x at the location where it permanently resides in memory.

**Unary increment and decrement operators** The unary `++` and `--` operators, respectively, increment or decrement the value of a variable by 1. There are 'pre' and 'post' variants for both operators that do slightly different things as explained below.

+   - `var++` increment 'post' variant
+   - `var--` decrement 'post' variant
+   - `++var` increment 'pre' variant
+   - `--var` decrement 'pre' variant

The following examples illustrate the use of increment and decrement operators on a variable not placed in an expression.

# ### EXAMPLE

```
```c
3. int i = 42;
   i++; /* increment contents of i, same as i = i + 1; */
        /* i is now 43 */
   i--; /* decrement contents of i, same as i = i - 1; */
        /* i is now 42 */
   ++i; /* increment contents of i, same as i = i + 1; */
        /* i is now 43 */
   --i; /* decrement contents of i, same as i = i - 1; */
        /* i is now 42 */
```
```

# ## Basic rules for using ++ and -- operators

+   - The operand must be a variable but not a constant or an expression.
+   - The operator `++` and `--` may precede or succeed the operand.

# ### EXAMPLES

```
```c
4. #include <stdio.h>
   int main()
   {
       int a=5, b=3;
       printf("\n %d", ++(a*b+2));
       return 0;
   }
```
```

**Output**

Compiler error - Lvalue required

```
```c
5. #include <stdio.h>
   int main()
   {
       printf("\n %d", ++2);
       return 0;
   }
```
```

**Output**

Compiler error - Lvalue required

It is to be noted that `i++` executes faster than `i = i + 1` because the expression `i++` requires a single machine instruction such as INR to carry out the increment operation whereas `i = i + 1` requires more instructions to carry out this operation.

**Pre- and post-variations of ++ and -- operators** The pre-and post- (`++` and `--`) operators differ in the value used for the operand when it is embedded inside expressions.

If it is a 'pre' operator, the value of the operand is incremented (or decremented) before it is fetched for computation. The altered value is used for computation of the expression in which it occurs.

A few examples are shown here to demonstrate the use of the increment and decrement operators for postfix and prefix operations in expressions.

# ### EXAMPLES

# ### 6. Postfix operation

![](bbox=[0.51, 0.514, 0.977, 0.605])

![](bbox=[0.51, 0.61, 0.977, 0.705])

# ### 7. Prefix operation

![](bbox=[0.51, 0.744, 0.977, 0.838])