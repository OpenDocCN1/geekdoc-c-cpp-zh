# Assignment, Formatting, and Interactive Input

The simplest expression in C++ is a single constant. In the following assignment statements, the operand to the right of the equal sign is a constant:

```
length = 25;
width = 17.5;
```

In these assignment statements, the value of the constant to the right of the equal sign is assigned to the variable on the left of the equal sign. Note that the equal sign in C++ doesn't have the same meaning as an equal sign in algebra. The equal sign in assignment statement tells the computer to determine the value of the operand to the right of the equal sign, and to store (or assign) that value in the location associated with the left of the equal sign. For example, the C++ statement length = 25; is read blank spaces in the assignment statement are inserted for readability only

Recall that a variable can be initialized when it's declared. If an initialization isn't done in the declaration statement, the variable should be assigned a value with an assignment statement or operation before it is used in any computation. Subsequent assignment statements, of course, can change the value assigned to a variable. For example, assume the following statements execute one after another, and slope not initialized when it was declared:

```
slope = 3.7;
slope = 6.28;
```

The first assignment statement assigns the value of 3.7 to the variable named slope. The next assignment statement causes the computer to assign a value of 6.28 to slope. The 3.7 that was in slope is overwritten with the new value of 6.28 because a variable can store only one value at a time. Sometimes it's useful to think of the variable to the left of each as a temporary parking spot in a huge lot. Just as a parking spot can be used by only one car at a time, each variable can store only one value at a time. "Parking" a new value in a variable automatically allows the program to remove any value there previously.

In addition to being a constant, the operand to the right of the equal sign in an assignment statement can be a variable or any other valid C++ expression. An expression is any combination of constants, variables, and function calls that can be evaluated to yield a result. Therefore, the expression in an assignment statement can be used to perform calculations using the arithmetic operators introduced in Section 2.4. The following are examples of assignment statements using expressions containing these operators:

```
sum = 3 + 7;
diff = 15 - 6;
product = . * 14.6;
tcount += 1;
newtotal = 38.3 + count;
taxes = .  06 * amount;
totalWeight = factor * weight;
average = sum / items;
slope = (y2 - y1) / (x2 - x1);
```