+   1. Stack before function call (each box represents 2 bytes)
+   2. Stack after function call
+   3. Stack after function begins execution
+   4. Stack after function terminates

Diagram of passing arguments using a stack. The stack grows through four stages. Before the call, the stack contains values 1890 and 2929. The call `fib(18, 50L);` pushes the arguments onto the stack: the long value 50L takes 4 bytes and the int value 18 takes 2 bytes. When the function begins execution, `tell` and `real` associate the formal arguments with the values on the stack. When the function terminates, the top of stack resets to its original position. Stack annotations include “top of stack (next addition goes here)” and “values placed on the stack earlier.”

```
void fib(int real, long tell)
{
  ...
}
```

Figure 9.3  Passing arguments by using a stack.

# Note

Classic K&R C does not allow you to initialize automatic arrays and structures, but it does allow you to initialize static arrays and structures. ANSI C and C++ allow you to initialize both kinds. But some older C++ translators use C compilers that are not fully ANSI C-compliant. If you are using such an implementation, you might need to use one of the three varieties of static storage classes for initializing arrays and structures.