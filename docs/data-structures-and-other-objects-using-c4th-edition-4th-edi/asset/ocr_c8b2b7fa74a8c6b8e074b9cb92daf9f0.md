Whenever we reach a right parenthesis, we combine the top two numbers (on the numbers stack) using the topmost operation (on the characters stack). In our example, we compute 6 + 9, yielding 15, and this number 15 is pushed back onto the numbers stack:

```
Characters read so far (shaded):
(( ( 6 + 9 ) / 3 ) * ( 6 - 4 )
```

![](bbox=[0.26, 0.26, 0.84, 0.35])

Notice that the leftmost operand (6 in this example) is the second number popped off the stack, so the correct evaluation is 6 + 9, not 9 + 6. But the order of the operands does matter for subtraction and division.

Next we simply continue the process: reading up to the next right parenthesis, pushing the numbers we encounter onto the numbers stack and pushing the operations we encounter onto the operations stack. When we reach the next right parenthesis, we combine the top two numbers using the topmost operation. Here's what happens in our example when we reach the second right parenthesis:

```
Characters read so far (shaded):
(( ( 6 + 9 ) / 3 ) * ( 6 - 4 )
```

![](bbox=[0.26, 0.54, 0.84, 0.64])

Again, the leftmost operand (15) is the second number popped off the stack, so the correct evaluation is 15/3, not 3/15. Continuing the process, we obtain:

```
Characters read so far (shaded):
(( ( 6 + 9 ) / 3 ) * ( 6 - 4 )
```

![](bbox=[0.26, 0.74, 0.84, 0.84])