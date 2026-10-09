# 5.4.4  Inline

As a general rule, a good programmer never writes the same code twice. You should write reusable functions. That way you minimise the amount of effort you have to make in testing your code.

Novice programmers often make the mistake of using the cut-and-paste features of their development environment as an alternative to writing functions. This is a very bad idea. It results in code that is hard to read and hard to test. If you detect a mistake in some code that has been manually cut and pasted into 100 other files, you are going to have to track down that error in lots of files.

> Tip: Write functions. Don’t use cut and paste.

However, from a performance point of view it is ever so slightly faster to run code that has been cut and pasted than it is to write code that has been divided into functions. The reason is that at the level of assembly language, calls to functions are turned into machine code CALL commands. The performance cost of calling a function is therefore equal to the cost of running the code for the function plus the cost of a CALL statement.

Most of the time this extra overhead of using functions is absolutely trivial and not worth considering. But every now and again, it is worth thinking about. The solution is not to stop writing functions: it is to tell the compiler to “inline” the functions. This means that you wish to use functions to write your code, but you are telling the compiler to generate the machine code as if you had used cut and paste. The net effect is that the machine code for your function is “copied and pasted” throughout your program by the compiler and so there is no need for CALL statements. In other words, you end up with the faster code you would get by cutting and pasting but without having to sacrifice the benefits of functions.

The **hornerFunction** examples discussed in Exercise 3.9.6 are best inlined. Here is one of the **hornerFunctions** with the **inline** keyword added.

```
```
 static  inline  double hornerFunction(
 double x,
 double a0,
 double a1) {
 return a0 + x*a1;
}
```
```

The optimisation can be justified in this special case because we use **hornerFunction** to compute **norminv** and we will be calling **norminv** a great deal in our Monte Carlo simulations. So getting these functions to be as fast as possible is worthwhile.