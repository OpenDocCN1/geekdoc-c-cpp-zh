The six relational operators exhaust the comparisons C++ enables you to make for numbers. If you want to compare two values to see which is the more beautiful or the luckier, you must look elsewhere.

Here are some sample tests:

```
~~~cpp
for (x = 20; x > 5; x--)   // continue while x is greater than 5
for (x = 1; y != x; ++x)   // continue while y is not equal to x
for (cin >> x; x == 0; cin >> x)   // continue while x is 0
~~~
```

The relational operators have a lower precedence than the arithmetic operators. That means this expression:

```
~~~cpp
x + 3 > y - 2        // Expression 1
~~~
```

corresponds to this:

```
~~~cpp
(x + 3) > (y - 2)    // Expression 2
~~~
```

and not to the following:

```
~~~cpp
x + (3 > y) - 2      // Expression 3
~~~
```

Because the expression (3 > y) is either 1 or 0 after the bool value is promoted to int, Expressions 2 and 3 are both valid. But most of us would want Expression 1 to mean Expression 2, and that is what C++ does.

# ## Assignment, Comparison, and a Mistake You'll Probably Make

Don't confuse testing the is-equal-to operator (==) with the assignment operator (=). This expression asks the musical question “Is musicians equal to 4?”:

```
~~~cpp
musicians == 4    // comparison
~~~
```

The expression has the value true or false. This expression assigns the value 4 to musicians:

```
~~~cpp
musicians = 4     // assignment
~~~
```

The whole expression, in this case, has the value 4 because that's the value of the left side. The flexible design of the for loop creates an interesting opportunity for error. If you accidentally drop an equals sign (=) from the == operator and use an assignment expression instead of a relational expression for the test part of a for loop, you still produce valid code. That's because you can use any valid C++ expression for a for loop test condition. Remember that nonzero values test as true, and zero tests as false. An expression that assigns 4 to musicians has the value 4 and is treated as true. If you come from a language, such as Pascal or BASIC, that uses = to test for equality, you might be particularly prone to this slip.

Listing 5.10 shows a situation in which you can make this sort of error. The program attempts to examine an array of quiz scores and stops when it reaches the first score that's not 20. It shows a loop that correctly uses comparison and then one that mistakenly uses assignment in the test condition. The program also has another egregious design error that