
## FIGURE 9.9 A Function to Play the Teddy Bear Game

## A Function Implementation

```cpp
bool bears(int initial, int goal, int increment, int n)
// Precondition: All parameters are non-negative integers.
// Postcondition: The method has determined whether it is possible to reach the goal in the
// following Teddy Bear game. In the game, your friend gives you a certain number of bears.
// The number of bears is called initial, and your goal is to end up with a particular number of
// bears, called the goal number. At any point in the game, you have two choices: (a) You can
// ask for (and receive) increment more bears, or (b) if you have an even number of bears,
// then you can give half of them back to your friend. Each time you do (a) or (b), that is called
// a step in the game.
// The return value is true if and only if the goal can be reached in n steps or fewer.
{
    if (initial == goal)
        return true;
    else if (n == 0)
        return false;
    else if (bears(initial+increment, goal, increment, n-1))
        return true;
    else if (((initial % 2 == 0) && bears(initial/2, goal, increment, n-1)))
        return true;
    else
        return false;
}
```

## Self-Test Exercises for Section 9.2

- 9. Suppose you call random_fractal with a width of 8 and an epsilon of 1. Then random_fractal will make two recursive calls, and each of those will make more calls, and so on until width is less than or equal to epsilon. How many total calls will be made of random_fractal, including the original call?

- 10. Draw a copy of the maze from Figure 9.6 on page 454, moving the magic tapestry to a more difficult location. Run the traverse_maze function, pretending that you are in this maze and following the function’s directions. (Do not peek over the walls.)

- 11. Revise the random_fractal function so that the movements of the midpoints are no longer random. Instead, the first midpoint should be moved upward by the amount width, the midpoints at the next level of recursion should be moved down by the amount width, the next level will move up again, then down, and so on.

- 12. Suppose that you are exploring a rectangular maze containing 10 rows and 20 columns. What is the maximum number of recursive calls that can be generated if you start at the entrance of the maze and call traverse_maze?

## 9.3 REASONING ABOUT RECURSION

> After a lecture on cosmology and the structure of the solar system, William James was accosted by a little old lady.
>
> "Your theory that the sun is the center of the solar system, and the earth is a ball which rotates around it has a very convincing ring to it, Mr. James, but it's wrong. I've got a better theory," said the little old lady.
>
> "And what is that," inquired James politely.
>
> "That we live on a crust of earth which is on the back of a giant turtle."
>
> Not wishing to demolish this absurd little theory by bringing to bear the masses of scientific evidence he had at his command, James decided to gently dissuade his opponent by making her see some of the inadequacies of her position.
>
> "If your theory is correct, madam," he asked, "what does this turtle stand on?"
>
> "You're a very clever man, Mr. James, and that's a very good question," replied the little old lady, "but I have an answer to it. And it is this: the first turtle stands on the back of a second, far larger, turtle, who stands directly under him."
>
> "But what does this second turtle stand on?" persisted James patiently.
>
> To this the little old lady crowed triumphantly. "It's no use, Mr. James—it's turtles all the way down."
>
> J. R. Ross
> Constraints on Variables in Syntax

In all our examples of recursive thinking, the series of recursive calls eventually reached a call that did not involve further recursion (that is, it reached a stopping case). If, on the other hand, every recursive call produces another recursive call, then a recursive call will, in theory, run forever. This is called infinite recursion. In practice, such a function will run until the computer runs out of memory for the activation records and terminates the program abnormally. Phrased another way, a recursive declaration should not be "recursive all the way down." Otherwise, like the lady's explanation of the solar system, a recursive call will never end, except perhaps in frustration.

In this section, we will show you how to reason about recursive functions, both to show that there is no infinite recursion and to show that a recursive function's results are correct. As an example, we'll start with a new recursive function called power that computes powers of the form x^n, where x is any double number and n is an integer. So, power(3.0, 2) is 3.0^2 (which is 9.0), and power(4.2, 3) is 4.2^3 (which is 74.088). For any nonzero value of x, the value of x^0 is defined to be 1, so for example power(9.1, 0) is 1. For a negative exponent, -n, the value returned is defined by:
x^-n = 1/x^n { x is any real number, and -n is a negative integer }

For example, power(3.0, -2) is 1/3.0^2 (which is 1/9). The only forbidden power is taking 0^0 when n is not positive. Here is the function's complete specification:

```cpp
double power(double x, int n);
// Precondition: If x is zero, then n must be positive.
// Postcondition: The value returned is x raised to the power n.
```

Our implementation begins by checking the precondition, and then deals with several cases. The first case, when n is non-negative, is easy. This case is computed by setting a local variable, product, to 1, and then repeatedly multiplying product by x. The repeated multiplication occurs n times, in the for-loop shown here:

```cpp
if (n >= 0)
{
    product = 1;
    for (count = 1; count <= n; ++count)
        product = product * x;
    return product;
}
```

To understand what is needed for a negative exponent, let's consider a concrete case. Suppose that we are computing power(3.0, -2), which must return the value 3.0^-2. But this value is equal to 1/3.0^2. Negative powers are the same as positive powers in the denominator. This means that if we know that the function returns the correct answer when n is positive, then we can calculate the correct value for power(3.0, -2) by the expression 1/power(3.0, 2). By thinking recursively, whenever n is negative, power can compute its answer with a recursive call, like this:

```cpp
return 1/power(x, -n); // When n is negative (and so -n is positive)
```

Remember, in this statement, n is negative (such as -2), so that -n is positive, and therefore, the recursive function call in the expression 1/power(x, -n) has a positive second argument. With a positive second argument, our power function makes no further recursive calls (i.e., a stopping case), and so the recursion ends.

This brings us to our first general technique for reasoning about recursion, which can be applied to the complete power function of Figure 9.10:

> **One-Level Recursion**
>
> Suppose that every case is either a stopping case or it makes a recursive call that is a stopping case. Then the deepest recursive call is only one level deep, and therefore no infinite recursion occurs.

## FIGURE 9.10 Implementation of the Power Function with Only One Level of Recursion

## A Function Implementation

```cpp
double power(double x, int n)
// Precondition: If x is zero, then n must be positive.
// Postcondition: The value returned is x raised to the power n.
// Library facilities used: cassert
{
    double product; // The product of x with itself n times
    int count;
    if (x == 0)
        assert(n > 0);
    if (n >= 0)
    {
        product = 1;
        for (count = 1; count <= n; ++count)
            product = product * x;
        return product;
    }
    else
        return 1/power(x, -n);
}
```

## Sample Results of the Function

| Call with these arguments | Return value of function call |
|---|---|
| x n | |
| 3.0 2 | 9.0 |
| 2.0 -3 | 0.125 |
| 4.1 0 | 1.0 |
| -2.0 3 | -8.0 |

www.cs.colorado.edu/~main/chapter9/powers.cxx WWW

## How to Ensure That There Is No Infinite Recursion

In general, recursive calls don't stop at just one level deep. A recursive call does not need to reach a stopping case immediately. Programmers have developed methods to reason about recursive calls that go beyond one level deep, based on the principles of mathematical induction. The reasoning can increase your confidence that a recursive function avoids infinite recursion. As an example to show that there is no infinite recursion, let's rewrite the function power so that it
