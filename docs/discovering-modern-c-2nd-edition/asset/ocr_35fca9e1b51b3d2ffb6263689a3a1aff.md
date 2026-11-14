semesters). The students, mostly from the mathematics department, plus some from the physics and engineering departments, often did not know C++ before the class were able to implement advanced techniques like expression templates (§5.3) by the end of the course. You can read this book at your own pace: straight to the point by following the main path or more thoroughly by reading additional examples and background information in Appendix A.

# The Beauty and the Beast

C++ programs can be written in so many ways. In this book, we will lead you smoothly to the more sophisticated styles. This requires the use of advanced features that might be intimidating at first but will become less so once you get used to them. Actually, high-level programming is not only more widely applicable but is usually equally or more efficient and readable.

We will give you a first impression with a simple example: gradient descent with constant step size. The principle is extremely simple: we compute the steepest descent of f(x) with its gradient, say g(x), and follow this direction with fixed-size steps to the next local minimum. Even the algorithmic pseudo-code is as simple as this description:

```
Algorithm 1: Gradient descent algorithm
Input: Start value x, step size s, termination criterion e, function f, gradient g
Output: Local minimum x
1 do
2 |x = x - s · g(x)
3 while |Δf(x)| >= e ;
```

For this simple algorithm, we wrote two quite different implementations. Please have a look and let it sink in without trying to understand the technical details.

Click here to view code image