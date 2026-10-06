# 5. Program Looping

In Objective-C, you can repeatedly execute a sequence of code in several ways. These looping capabilities are the subject of this chapter, and they consist of the following:

The `for` statement

The `while` statement

The `do` statement

We start with a simple example: counting numbers.

If you were to arrange 15 marbles into the shape of a triangle, you would end up with an arrangement that might look something like [Figure 5.1].

# Figure 5.1. Triangle arrangement example

![](bbox=[0.453, 0.566, 0.542, 0.646])

The first row of the triangle contains one marble, the second row contains two marbles, and so on. In general, the number of marbles required to form a triangle containing $n$ rows would be the sum of the integers from 1 through $n$. This sum is known as a *triangular number*.

If you started at 1, the fourth triangular number would be the sum of the consecutive integers 1–4 ($1 + 2 + 3 + 4$), or 10.

Suppose you wanted to write a program that calculated and displayed the value of the eighth triangular number. Obviously, you