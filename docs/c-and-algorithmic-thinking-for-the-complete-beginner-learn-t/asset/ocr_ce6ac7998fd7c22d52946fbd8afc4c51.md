# # Chapter 7

# ## Operators

# ### 7.1　The Value Assignment Operator

The most commonly used operator in C++ is the value assignment operator (=). For example, the C++ statement

```
x = 5;
```

assigns a value of 5 to variable x.

As you read in Chapter 5, this is equivalent to the left arrow used in flowcharts.

![](bbox=[0.423, 0.352, 0.601, 0.434])

Probably the left arrow used in a flowchart is more convenient and clearer than the value assignment operator (=) sign because it shows in a more graphical way that the value or the result of an expression on the right is assigned to a variable on the left.

Be careful! The (=) sign is not equivalent to the one used in mathematics. In mathematics, the expression x = 5 is read as “x is equal to 5.” However, in C++ the expression x = 5 is read as “assign the value 5 to x” or “set x equal to 5.” They look the same but they act differently!

In mathematics, the following two lines are equivalent:

```
x = y + z
y + z = x
```

The first one can be read as “x is equal to the sum of y and z” and the second one as “the sum of y and z is equal to x.”

On the other hand, in C++, the following two statements are definitely **not** equivalent. In fact, the second one is considered wrong!

```
x = y + z;
y + z = x;
```

The first statement seems quite correct. It can be read as “Set x equal to the sum of y and z” or “Assign the sum of y and z to x.”

But what about the second one? Think! Is it possible to assign the value of x to y + z? The answer is obviously a big “NO!”