two numbers (symbols) that are popped from the stack, and the result is pushed onto the stack. For instance, the postfix expression

```
6 5 2 3 + 8 + 3 + *
```

is evaluated as follows:

The first four symbols are placed on the stack. The resulting stack is

![](bbox=[0.435, 0.243, 0.705, 0.353])

Next, a ‘+’ is read, so 3 and 2 are popped from the stack, and their sum, 5, is pushed.

![](bbox=[0.435, 0.433, 0.705, 0.543])

Next, 8 is pushed.

![](bbox=[0.435, 0.623, 0.705, 0.723])

Now a ‘*’ is seen, so 8 and 5 are popped, and 5 * 8 = 40 is pushed.

![](bbox=[0.435, 0.813, 0.705, 0.923])