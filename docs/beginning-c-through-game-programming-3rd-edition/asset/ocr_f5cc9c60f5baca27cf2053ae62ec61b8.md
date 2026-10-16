of lives a player has, and I also increment the number of lives. However, I perform this calculation in two different ways. The first time, I use the prefix increment operator.

```
int bonus = ++lives * 10;
```

The prefix increment operator increments a variable before the evaluation of a larger expression involving the variable. ++lives * 10 is evaluated by first incrementing lives, and then multiplying that result by 10. Therefore, the code is equivalent to 4 * 10, which is 40, of course. This means that now lives is 4 and bonus is 40.

After setting lives back to 3, I calculate bonus again, this time using the postfix increment operator.

```
bonus = lives++ * 10;
```

The postfix increment operator increments a variable after the evaluation of a larger expression involving the variable. lives++ * 10 is evaluated by multiplying the current value of lives by 10. Therefore, the code is equivalent to 3 * 10, which is 30, of course. Then, after this calculation, lives is incremented. After the line is executed, lives is 4 and bonus is 30.

C++ also defines the decrement operator, --. It works just like the increment operator, except it decrements a variable. It comes in the two flavors (prefix and postfix) as well.

# Dealing with Integer Wrap Around

What happens when you increase an integer variable beyond its maximum value? It turns out you don’t generate an error. Instead, the value “wraps around” to the type’s minimum value. Next up, I demonstrate this phenomenon. First I assign score the largest value it can hold.

```
score = 4294967295;
```

Then I increment the variable.

```
++score;
```

As a result, score becomes 0 because the value wrapped around, much like a car odometer does when it goes beyond its maximum value (see Figure 1.7).

Decrementing an integer variable beyond its minimum value “wraps it around” to its maximum.