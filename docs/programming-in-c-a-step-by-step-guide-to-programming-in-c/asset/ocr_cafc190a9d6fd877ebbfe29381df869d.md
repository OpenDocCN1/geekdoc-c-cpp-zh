4. State whether the following statement is correct or not. (Correct/Incorrect)

```
if(a<4<c)

b=c;
```

# 2.5 The Conditional Operator

The Conditional operator (ternary operator) pair “?:” is available in C to construct conditional expressions of the form

```
expr1?expr2:expr3
```

where *expr1*, *expr2* and *expr3* are expressions.

The operator ?: works as follows: *expr1* is evaluated first. If it is nonzero(true), then the expression *expr2* is evaluated and becomes the value of the expression. If *expr1* is false, *expr3* is evaluated and its value becomes the value of the expression. For example, consider the following statements:

```
a=100;

b=200;

c=(a>b)?a:b;
```

In this example, c will be assigned the value of b. This can be achieved using the if..else statements as follows:

```
if(a>b)

c=a;

else

c=b;
```