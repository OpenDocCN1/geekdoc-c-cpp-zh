As the running example, consider the following code:

```
~~~csharp
int max = int.MaxValue;
int res = max + 1;

Console.WriteLine(res);
~~~
```

We already know this overflows results in -2147483648. Take a look at the IL code in Figure 5.12 to see what's going on here.

![](bbox=[0.066, 0.278, 0.64, 0.512])

FIGURE 5.12 The add instruction doesn't protect against overflow.

The resulting add instruction allows overflow conditions, causing the observed behavior. Various options exist to turn on overflow checking. The first one is to use the checked keyword as a unary expression:

```
~~~csharp
int max = int.MaxValue;
int res = checked(max + 1);

Console.WriteLine(res);
~~~
```

Here, only the arithmetic operations in the expression surrounded by the checked(...) syntax are subject to overflow checking. To accomplish this, the compiler has emitted different code for the addition using the add.ovf instruction instead, as shown next. But first, let's see what the runtime behavior of the code is now. Figure 5.13 shows the result of running this code in the Visual Studio debugger.

The result is an exception that, if left unhandled, results in program termination. We discuss exceptions thoroughly, but the OverflowException is likely something you want to leave unhandled. If you opted in to arithmetic overflow checking, it's likely because you wanted to avoid disaster in case of an overflow, and you'll be better off having the program terminate on the spot instead of trying to recover from it. Overflow should be