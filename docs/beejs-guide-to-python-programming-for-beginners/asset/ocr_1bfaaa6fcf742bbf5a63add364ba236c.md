# 14.7 Catching Multiple Exceptions

Problem-solving step: Understanding the Problem

What if your try block throws multiple exceptions?

Turns out you can catch multiple exceptions just by having multiple except clauses.

Let's try a program that divides a number by another:

```
```python
x, y = input('Enter two numbers separated by a space: ').split()

x = int(x)
y = int(y)

print(f'{x} / {y} == {x / y}')
```
```

What are the exceptions that can be thrown?

Good question. Although there is a list of built-in exceptions³, it's not immediately obvious which one gets raised when.

The easy thing to do is try it in the REPL. But try what?

Think like a villain. What are the things that can go wrong? What kinds of bad input can you pass this program?

Give it some thought. I count four things that can go wrong with bad user input. Can you see them?

Well, we're taking input, running it through .split(), and then assigning the results into two variables. So the split() better return a list of length 2, or something bad is going to happen.

I'm going to put that line of code into the REPL and see what it says if I enter something that's not two numbers separated by a space.

```
```
>>> x, y = input("Enter 2 numbers: ").split()
Enter 2 numbers: 1
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: not enough values to unpack (expected 2, got 1)
```
```

Check it out! I entered a single number, and it raised ValueError exception (with a message saying there weren't enough values).

Let's try too many values:

```
```
>>> x, y = input("Enter 2 numbers: ").split()
Enter 2 numbers: 1 2 3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: too many values to unpack (expected 2)
```
```

ValueError again! That means we can do something like this to catch it:

```
```python
try:
    x, y = input('Enter two numbers separated by a space: ').split()
    x = int(x)
    y = int(y)
    print(f'{x} / {y} == {x / y}')
except ValueError:
    print("That's not two numbers separated by a space!")
```
```