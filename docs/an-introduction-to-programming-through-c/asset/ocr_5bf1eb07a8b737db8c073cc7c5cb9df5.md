# Chapter 8

# Computing common mathematical functions

In this chapter we will see ways to compute some common mathematical functions, such as trigonometric functions, square roots, exponentials and logarithms. We will also see how to compute the greatest common divisor of two numbers using Euclid's algorithm. This is one of the oldest interesting algorithm, invented well before computers were even conceived.

The main statement in all the programs of the chapter will be a looping statement. You could consider this chapter to be an extension of the previous, giving more ways in which loop statements can be used.

Some of the material in this chapter requires somewhat deep mathematics. We will state the relevant theorems, and try to explain intuitively why they might be true. The precise proofs are outside the scope of this book.

# 8.1 Taylor series

Suppose we wish to compute f(x) for some function f, such as say f(x) = sin(x). Suppose we know how to compute f(x0) for some fixed x0. Suppose that the derivative f' of f and the derivative f'' of f' and so on exist at x0, and we can evaluate these. Then if x is reasonably close to x0 then f(x) equals the sum of the Taylor series of f at x0. The ith term of the Taylor series is f^i(x0)(x - x0)^i / i!, in which f^i is the function obtained from f by taking derivative i times. Thus we have:

f(x) = f(x0) + f'(x0)(x - x0) + f''(x0)(x - x0)^2 / 2! + f^m(x0)(x - x0)^3 / 3! + ⋯

In the typical scenario, we only compute and sum the first few terms of the series, and that gives us a good enough estimate of f(x). The general theory of this is discussed in standard mathematics texts and is outside our scope. However, you may recognize the first two terms as coming from a tangent approximation of the curve, as shown in Figure 8.1. The value of f(x) equals (the length of) FD. We approximate this by FC, which in turn is FB + BC = EA + (BC/AB)AB = f(x0) + f'(x0)·(x - x0).