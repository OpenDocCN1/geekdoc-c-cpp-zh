# Strings in Python

Python is excellent for using words and sentences within programs. Different strings (sequences of characters) can be joined together, or individual parts of them can be selected and pulled out.

> SEE ALSO

< 54–55 Strings and lists

< 110–111 Types of data

# Creating a string

A string might include letters, numbers, symbols, or spaces. These are all called characters. Strings can be placed in variables.

![](bbox=[0.525, 0.235, 0.936, 0.513])

+   > Strings in variables
Variables can store strings. Type these two strings into the variables "a" and "b".

```
>>> a = 'Run!
>>> b = 'Aliens are coming.'
```

The quotation marks indicate the variable contains a string

# Adding numbers together

Adding numbers together creates a new number. In the same way, when two strings are added together, one string joins on to the other one.

> EXPERT TIPS
Length of a string

```
>>> c = a + b
>>> print(c)
Run! Aliens are coming.
```

The "len()" function is used to find out the length of a string. Python counts all of the characters, including spaces, to give the total number of characters in a string.

+   > Adding strings together
The "+" symbol joins one string to another, and the answer becomes the variable "c".

Calculates the length of the string in variable "a" ("Run")

```
>>> c = b + ' ' Watch out!
>>> print(c)
Aliens are coming. Watch out! Run!
```

```
>>> len(a)
4
>>> len(b)
18
```

The string in variable "b" ("Aliens are coming.") is 18 characters long

+   > Adding another string in between\New string can also be added between two strings. Try the example above.

A new string is added to variable "c" appears in the middle of the message