this section by talking about numbers; we'll cover the others in later chapters.

Before I forget, I should mention that Python doesn't have strong coded types; that is, a variable can be used as an integer, a float, a string, or whatever. Python will determine what is needed as its runs. See below:

# Listing 5.3: Weak coding types

```
"""
>>> x = 12
>>> y = "lumberjack"
>>> x
12
>>> y
'lumberjack'"""
```

Other languages often require the programmer to decide what the variable must be when it is initially created. For example, C would require you to declare "x" in the above program to be of type *int* and "y" to be of type *string*. From then on, that's all those variables can be, even if later on you decide that they should be a different type.

That means you have to decide what each variable will be when you start your program, i.e. deciding whether a number variable should be an integer or a floating-point number. Obviously you could go back and change them at a later time but it's just one more thing for you to think about and remember. Plus, anytime you forget what type a variable is and you try to assign the wrong value to it, you get a compiler error.

# ### 5.3 Python Numbers

Python can handle normal long integers (max length determined based on the operating system, just like C), Python long integers (max length dependent on available memory), floating point numbers (just like C doubles), octal and hex numbers, and complex numbers (numbers with an imaginary component). Here are some examples of these numbers:

+   * integer: 12345, -32