understand how C code may have been changed in the past to provide faster execution time for a given target. Like most optimizations at the C source code level, it can lead to the purpose of the source code being obscured.

# Loop invariant analysis

Loop invariant analysis looks for expressions that are constant within the loop body and moves them outside the loop body. Thus, for example,

```
for (int j=0;j<100;j++)
{
for (int i=0; i<100; +++)
{
const int b = j * 200;
q[i] = b;
}
}
```

In this example, the parameter j is constant within the loop body for parameter i. Thus, the compiler can easily detect this and will move the calculation of b outside the inner loop and generate the following code:

```
for (int j=0;j<100;j++)
{
const int b = j * 200;
for (int i=0; i<100; +++)
{
q[i]= b;
}
}
```

This optimized code removes thousands of unnecessary calculations of b, where j, and thus b, are constant in the inner loop. However, consider the case where b is an external to the function, a global variable, instead of a local variable. For example:

```
int b;
void some_func(void)
{
for (int j=0;j<100;j++)
{
for (int i=0; i<100; +++)
b = j * 200;
q[i]= b;
}
}
}
```