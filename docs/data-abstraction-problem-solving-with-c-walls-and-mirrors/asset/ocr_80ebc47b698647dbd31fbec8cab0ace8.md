# Recursion That Returns a Value 53

This function fits the model of a recursive function given earlier in this chapter as:

+   1. One action of fact is to call itself.
2. At each recursive call, the integer factorial you need to compute is diminished by 1!.
3. The function handles the factorial of 0 differently from all the other factors: It does not generate a recursive call. Rather, you know that fact(0) is 1. Thus, the base case occurs when n is 0.
4. Given that n is nonnegative, 2 of this list assures you that you will always reach the base case.

fact satisfies the four criteria of recursive solution

> Note: A recursive algorithm has a base case, which you know directly without making any recursive calls. Without a base case, a recursive function will generate an infinite sequence of calls.

The function reacts as its precondition a nonnegative value of n. At the time of the recursive fact(n-1), n is positive, so the recursive call satisfies fact's precondition, you can expect that fact(n-1) will return the factorial of n−1. Therefore, fact(n-1) is the factorial of n. Chapter 5 uses mathematical induction to prove that fact(n) returns the factorial of n.

If you violated fact-3, the function would not behave correctly. That is, if the calling passed a negative value an infinite sequence of recursive calls—terminated only by a system-defined limit—would occur, and the function would never reach the base case. For example, fact(-4) would call fact(-6), and so on.
The function should ideally test itself by testing for negative n. If n < 0, the function could crash, either return 0 or set an error flag. Appendix B discusses error checking in Sections B.2 “Style” and B.5 “Full-Safe Programming”; you might want to review that discussion at this time.
at an intuitive level, it should be clear that the function implements the recursive definition of factorial. Now consider the mechanisms of executing this recursive function. The logic is straightforward, except for perhaps in the else case. This recursion can be explained as:

Violating fact precondition causes “infinite” recursion

+   1. Each operand of the product n * fact(n−1) is evaluated.
2. The second operand—fact(n−1)—is a call to fact. Although this is a recursive call (the function fact calls the function fact), there is nothing special about it. Imagine substituting a call to another function—the standard function abs, for example—for the recursive call to fact. The principle is the same: Evaluate the function.

In theory, evaluating a recursive function is no more difficult than evaluating a nonparametric function. However, manual bookkeeping can quickly get out of hand. The next section introduces a systematic way to trace the actions of a recursive function. For a computer, the bookkeeping is simple but can use more memory than is allocated for such a task.

# Question 1 The function computes the sum of the first n ≥ 1 integers. how this function satisfies the properties of a recursive function.

```
/// computes the sum of the integers from 1 through n.
@pre n > 0.
@post "None.\n@param n positive integer.
@return the sum 1 + 2 + . . + n /
```