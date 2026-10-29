
computer turns its attention to the top sheet of paper on the stack. This sheet contains the partially completed computation that is waiting for the recursive computation that just ended. Thus, it is possible to proceed with that suspended computation. When that suspended computation ends, the computer discards that sheet of paper and the suspended computation that is below it on the stack becomes the computation on top of the stack. The computer turns its attention to the suspended computation that is now on the top of the stack, and so forth. The process continues until the computation on the bottom sheet is completed. Depending on how many recursive calls are made and how the function definition is written, the stack may grow and shrink in any fashion. Notice that the sheets in the stack can only be accessed in a last-in/first-out fashion, but that is exactly what is needed to keep track of recursive calls. Each suspended version is waiting for the completion of the version directly above it on the stack.

Needless to say, computers do not have stacks of paper. This is just an analogy. The computer uses portions of memory rather than pieces of paper. The content of one of these portions of memory (“sheets of paper”) is called an **activation frame**. These activation frames are handled in the last-in/first-out manner we just discussed. (These activation frames do not contain a complete copy of the function definition, but merely reference a single copy of the function definition. However, an activation frame contains enough information to allow the computer to act as if the activation frame contained a complete copy of the function definition.)

## Stack

A stack is a last-in-first-out memory structure. The first item referenced or removed from a stack is always the last item entered into the stack. Stacks are used by computers to keep track of recursion (and for other purposes).

## PITFALL: Stack Overflow

There is always some limit to the size of the stack. If there is a long chain in which a function makes a recursive call to itself, and that call results in another recursive call, and that call produces yet another recursive call, and so forth, then each recursive call in this chain will cause yet another active frame to be placed on the stack. If this chain is too long, the stack will attempt to grow beyond its limit. This is an error condition known as a **stack overflow**. If you receive an error message that says “stack overflow,” it is likely that some function call has produced an excessively long chain of recursive calls. One common cause of stack overflow is infinite recursion. If a function is recursing infinitely, then it will eventually try to make the stack exceed any stack size limit.

efficiency

A recursively written function that is not tail recursive will usually run slower and use more storage than an equivalent iterative version. The computer must do a good deal of work manipulating the stack in order to keep track of the recursion. However, since the system does all this for you automatically, using recursion can sometimes make your job as a programmer easier by producing code that is easier to understand.

## Self-Test Exercises

- 6. If your program produces an error message that says "stack overflow," what is a likely source of the error?
- 7. Write an iterative version of the function cheers defined in Self-Test Exercise 1.
- 8. Write an iterative version of the function defined in Self-Test Exercise 2.
- 9. Write an iterative version of the function defined in Self-Test Exercise 3.
- 10. Trace the recursive solution you made to Self-Test Exercise 4.
- 11. Trace the recursive solution you made to Self-Test Exercise 5.

## 13.2 Recursive Functions That Return a Value

> To iterate is human, to recurse divine.
> 
> ANONYMOUS

## General Form for a Recursive Function That Returns a Value

The recursive functions you have seen thus far are all void functions, but recursion is not limited to void functions. A recursive function can return a value of any type. The technique for designing recursive functions that return a value is basically the same as that for void functions. An outline for a successful recursive function definition that returns a value is as follows:

- One or more cases in which the value returned is computed in terms of calls to the same function (that is, using recursive calls). As was the case with void functions, the arguments for the recursive calls should intuitively be "smaller."
- One or more cases in which the value returned is computed without the use of any recursive calls. These cases without any recursive calls are called base cases or stopping cases (just as they were with void functions).

## EXAMPLE: Another Powers Function

Chapter 3 introduced the predefined function pow that computes powers. For example, pow(2.0, 3.0) returns 2.0³, so the following sets the variable result equal to 8.0:

```
double result = pow(2.0, 3.0);
```

The function pow takes two arguments of type double and returns a value of type double. Display 13.3 contains a recursive definition for a function that is similar but that works with the type int rather than double. This new function is called power. For example, the following will set the value of result2 equal to 8, since 2³ is 8:

```
int result2 = power(2, 3);
```

Our main reason for defining the function power is to have a simple example of a recursive function, but there are situations in which the function power would be preferable to the function pow. The function pow returns a value of type double, which is only an approximate quantity. The function power returns a value of type int, which is an exact quantity. In some situations, you might need the additional accuracy provided by the function power.

The definition of the function power is based on the following formula:

xⁿ is equal to xⁿ⁻¹ × x

Translating this formula into C++ says that the value returned by power(x, n) should be the same as the value of the expression

```
power(x, n - 1)*x
```

The definition of the function power given in Display 13.3 does return the following value for power:

(x, n) provided n > 0.

The case where n is equal to 0 is the stopping case. If n is 0, then power(x, n) simply returns 1 (since x⁰ is 1).

Let’s see what happens when the function power is called with some sample values. First consider the following simple expression:

```
power(2, 0)
```

When the function is called, the value of x is set equal to 2, the value of n is set equal to 0, and the code in the body of the function definition is executed. Since the value of n is a legal value, the if-else statement is executed. Since this value of n is not greater than 0, the return statement after the else is used, so the function call returns 1. Thus, the following would set the value of result3 equal to 1:

```
int result3 = power(2, 0);
```

## Display 13.3 The Recursive Function power

```
1 //Program to demonstrate the recursive function power.
2 #include <iostream>
3 #include <cstdlib>
4 using std::cout;
5 using std::endl;

6 int power(int x, int n);
7 //Precondition: n >= 0.
8 //Returns x to the power n.

9 int main()
10 {
11     for (int n = 0; n < 4; n++)
12         cout << "3 to the power " << n
13             << " is " << power(3, n) << endl;
14
15     return 0;
16 }

17 //uses iostream and cstdlib:
18 int power(int x, int n)
19 {
20     if (n < 0)
21     {
22         cout << "Illegal argument to power.\n";
23         exit(1);
24     }
25     if (n > 0)
26         return ( power(x, n - 1) * x );
27     else // n == 0
28         return (1);
```

## Sample Dialogue

```
3 to the power 0 is 1
3 to the power 1 is 3
3 to the power 2 is 9
3 to the power 3 is 27
```

### 1.1 认识三角形

观察图片，你能发现哪些三角形？

![](img/c76bba8c1d927f399768ffe2ab5f5bee_623_0.png)

由不在同一条直线上的三条线段首尾顺次相接所组成的图形叫做三角形（triangle）。

如图1-1，线段AB，BC，CA是三角形的边，点A，B，C是三角形的顶点。∠A，∠B，∠C是相邻两边组成的角，叫做三角形的内角，简称三角形的角。

三角形用符号"△"表示，如图1-1的三角形记作"△ABC"，读作"三角形ABC"。

△ABC的三边，有时也用a，b，c来表示。如图1-1，顶点A所对的边BC用a表示，边CA、边AB分别用b、c来表示。
