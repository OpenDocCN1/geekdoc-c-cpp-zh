# Putting answers in variables

If variables are assigned number values, you can use them within sums. When a sum is assigned to a variable, the answer goes into the variable, but not the sum.

# Do a simple addition

This program adds together the variables "ants" and "spiders", and puts the answer into the variable "bugs".

```
>>> ants = 22
>>> spiders = 35
>>> bugs = ants + spiders
>>> print (bugs)
```

![](bbox=[0.043, 0.215, 0.477, 0.315])

Adds the values of the two variables together

Prints the value in "bugs"

# Change the value of a variable

Change the value of the "ants" or "spiders" variable. Add the variables together and put the answer in the variable "bugs".

# Skipping the assignment

If the sum is not assigned to the variable "bugs", even if the value of "ants" and "spiders" changes, the value of bugs,

```
>>> ants = 22
>>> spiders = 18
>>> bugs = ants + spiders
>>> print (bugs)
```

Change the value in "spiders"

```
>>> ants = 11
>>> spiders = 17
>>> print (bugs)
```

Prints the value in "bugs"

Add the variables together

The answer changes

The answer hasn't changed (it's still 18 + 22)

# Random numbers

To pick a random number, you first need to load the "randint" function into Python. To do this, use the "import" command. The "randint() function is already programmed with code to pick a random integer (whole number).

> REMEMBER
Random block

The "randint()" function works like the "pick random" block in Scratch. In Scratch, the lowest and highest possible numbers are typed into the windows in the block. In Python, they are put in brackets, separated by a comma.

Adds the "randint() function

```
>>> from random import randint
>>> randint(1, 6)
```

Picks a random number between 1 and 6

```
pick random 1 to 6
```

3 has been picked at random

A Whole numbers

Roll the die

The "randint()" function picks a random number between the two numbers in brackets. In this program, "randint(1, 6)" picks a value between 1 and 6.

Both the Python "randint()" function and the Scratch block pick a random whole number—the result is never in decimals.