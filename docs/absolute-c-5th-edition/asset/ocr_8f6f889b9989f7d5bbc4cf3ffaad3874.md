# CHAPTER 13 Recursion

If the function returns a value, all you need to check is that the following properties are satisfied:

# criteria for functions that return a value

+   1. There is no infinite recursion. (A recursive call may lead to another recursive call, which may lead to another, and so forth, but every such chain of calls eventually reaches a stopping case).
2. Each stopping case returns the correct value for that case.
3. For the cases that involve recursion: if all recursive calls return the correct value, then the final value returned by the function is the correct value.

For example,

+   1. There is no infinite recursion: The second argument to power(x, n) is decreased by 1 in each recursive call, so any chain of recursive calls will eventually reach the case power(x, 0), which is the stopping case. Thus, there is no infinite recursion.
2. Each stopping case returns the correct value for that case: A call of the form power(x, 0) always returns 1, and the correct value for x^n is 1. So the stopping case returns the correct value.
3. For the cases that involve recursion, if all recursive calls return the correct value, then the final value returned by the function is the correct value. The only case that recursion is when n > 1. When n > 1, power(x, n) returns

power(x, n - 1) * x

To see that the correct value is returned, note that if power(x, n) returns the correct value, then power(x, n-1) returns x^(n-1) and so power(x, 0) returns 1.

x^0 * x

is x^n, which is the correct value for power(x, n).

That is all need to be sure that the definition of power is correct. (The preceding technique is known as mathematical induction, a concept that you may have heard about in a mathematics class. However, you do not need to be familiar with the mathematical induction in order to use this technique.)

We have three criteria to use in checking the correctness of a recursive function that returns a value. Basically the same rules can apply to a recursive void function. If you show that your recursive function satisfies the following three criteria, then you will know that your void function performs perfectly:

# criteria for void functions

+   1. There is no infinite recursion.
2. Each stopping case performs the correct action for that case.
3. For each of the cases that involve recursion, if all recursive calls perform their actions correctly, then the entire case performs perfectly.

# Binary Search

This subsection develops a recursive function that searches an array to determine whether it contains a specified value. For example, the array may contain a list of numbers for credit cards that are no longer valid. Store clerk needs to search the list to see if a customer's card is valid or invalid.