# 4.5 EXECUTION OF RECURSIVE CALLS

Let us now see how recursive calls are executed. At every recursive call, all reference parameters and local variables are pushed onto the stack along with the function value and return address. The data is conceptually placed in a stack frame, which is pushed onto the system stack. A stack frame contains four different elements:

+   1. The reference parameters to be processed by the called function
+   2. Local variables in the calling function
+   3. The return address
+   4. The expression that is to receive the return value, if any

Consider the following two lines from the Factorial() function in Program Code 4.2:

```
if(n <= 1) return 1;
else return n * Factorial(n - 1);
```

Consider the first call as Factorial(4). Now,

+   1. n = 4
+   Hence, statement 2, which is a recursive call, is executed.
+   Push 4 onto the stack and call Factorial(4 - 1).

![](bbox=[0.36, 0.5, 0.75, 0.58])

+   2. n = 3
+   Hence, push 3 onto the stack and call Factorial(2).

![](bbox=[0.36, 0.67, 0.77, 0.73])

+   3. n = 2
+   Hence, push 2 onto the stack and call Factorial(1).

![](bbox=[0.36, 0.84, 0.77, 0.91])