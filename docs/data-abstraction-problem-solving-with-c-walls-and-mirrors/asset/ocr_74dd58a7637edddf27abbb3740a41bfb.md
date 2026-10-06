# CHAPTER 2 Recursion: The Mirrors

```
if (word is in the first half of aDictionary)
    search(first half of aDictionary)
else
    search(second half of aDictionary)
```

Writing the solution to a function allows several important observations:

+   1. One of the actions of the function is to call itself; that, the function search calls the function search. This is what makes the solution recursive. The strategy is to split dictionary in half, which determines half calls, and apply the same strategy to the appropriate half.
2. Each call to the search made from within the function passes a dictionary that is one-half the size of the previous dictionary. That is, at each successive call to search(dictionary), word, the size of dictionary is cut in half. The function solves the problem by solving another problem that is identical in nature but smaller in size.
3. There is some problem which handles differently from all others. When aDictionary contains only a single page, use another approach: Searching a one-page dictionary is the base case of the search problem. When you reach the base, the recursive calls stop and you solve the problem directly.
4. The manner in which the size of problem diminishes ensures that you will eventually reach the base.

A recursive function calls itself

Each recursive call identifies an identical, but smaller, problem

A test for the base case enables the recursive calls to stop

Eventually one of the smaller problems becomes the base case

These facts describe the general form of a recursive solution. Though not all recursive solutions follow these criteria as this solution does, the differences are far greater than differences. If you attempt to construct a new recursive solution, you should keep in mind the following questions:

![](bbox=[0.118, 0.503, 0.203, 0.603])

> Note: Four questions for constructing recursive solutions
1. How can you define the problem in a smaller problem of the same type?
2. How does each recursive call diminish the size of the problem?
3. What instance of the problem can serve as the base case?
4. As the problem diminishes, will you reach this base case?

Now consider relatively simple problems: computing the factorial of a number and writing a string backward. Their recursive solutions further illustrate the points raised by the solution to the dictionary search problem. These examples also illustrate the difference between a recursive valued function—which returns a value—and a recursive function.

# 2.2 Recursion Returns a Value

The mechanics of recursion are clearer when the recursive function returns a value instead of just performing an action, and we examine in detail.

# 2.2.1 A Recursive Valued Function: The Factorial of n

Computing the factorial of an integer n is a good example because its recursive solution is easy to understand and nearly fits the mold described earlier. However, because the problem has a simple and efficient iterative solution, you should not use the recursive solution in practice.

```
factorial(n) = n * (n - 1) * (n - 2) ·· * 1 for an integer n > 0
factorial(0) = 1
```

Do not use recursion if a problem has a simple, efficient iterative solution

An iterative definition of factorial

![](bbox=[0.138, 0.713, 0.203, 0.783])