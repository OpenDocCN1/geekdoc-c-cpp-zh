# Chapter 1 ■ Algorithm Basics 11

> **NOTE** It's important to remember that Big O notation is just intended to give you idea of an algorithm's theoretical behavior. Your results in practice may be different. For example, suppose an algorithm's performance is O(N), but if you don't ignore the constants, the actual number of steps executed is something like 100,000,000 + N. Unless N is real, you may not be able to safely ignore the constant.

# Common Runtime Functions

When you study the runtime of algorithms, some functions occur frequently. The following sections give you some examples of a few of the most common functions. They also give you some perspective that you'll know, for example, whether an algorithm with O(N³) performance is reasonable.

# 1

An algorithm with O(1) performance takes a constant amount of time no matter how big the problem is. These sorts of algorithms tend to perform relatively trivial tasks because they cannot even look at all the inputs in O(1) time.

For example, the quicksort algorithm needs to pick a number that is in an array of values. Ideally, that number should be somewhere in the middle of all the values in the array, but there is no easy way to tell which number might fall nicely in the middle. (For example, if the numbers are evenly distributed between 1 and 100, 50 would make a good dividing number.) The following algorithm shows one approach for solving this problem:

```
Integer DividingPoint(Integer: array[])nnumber1 = array[]
number2 = array[last index of array]
number3 = array[last index of array] / 2
```

```
if <number1 is between number2 and number3> Return number1
if <number2 is between number1 and number3> Return number2
Return number3
```

MiddleValue picks the values at the beginning, and the end, of the array, compares them, and returns whichever lies between the other two. This may not be the best item to pick out of the array, but there's a decent chance that it's not too terrible a choice.

Because this algorithm performs only a few steps, it has O(1) performance and its runtime is independent of the number of inputs N. (Of course, this algorithm doesn't really stand alone. It's just a small part of a more complicated algorithm.)