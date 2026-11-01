Ignoring the *objects for now, look at all those keyword arguments... in the docs, they have = followed by some value. This indicates the default value if you don't specify one otherwise. In other words, they're optional keyword arguments.

You can see that print() ends each line with a newline \n unless we tell it to end the line with some other string.

For now, it's enough to know that these exist and how to call them. Later on, we'll talk about how to write our own.

# 10.10 Interlude: Evaluation Strategies

If you don't want to read this section, it's OK to skip. But it's more fun if you read it.

Different languages have different behaviors when it comes to passing arguments to functions.

Some of them make copies of the values. Some of them just make it so the parameter name is an alias for the argument name. Some of them give you the option through some keyword.

How the programming language does this is called it's evaluation strategy.

Three very common ones are:

+   - **Call by Sharing:** This is what Python does. When you call a function, the parameters become references to the same objects as their corresponding arguments. This means that if, inside the function, you change the thing the parameter refers to, you'll see that change reflected out in the caller. However, if you assign a new value into a parameter, you will not see the change.

```
```python
def foo(x):
    # Modify the passed-in object. Caller will see this change.
    x[1] = 99

    # Assign a new list into x. The caller will _not_ see this change.
    x = [4, 5, 6]

a = [1, 2, 3]

foo(a)
print(a)  # [1, 99, 3]
```
```

+   - **Call by Value:** a copy of the argument is made and stored in the parameter. The C programming language, among others, uses this one. (Sometimes people say Python uses Call by Value, but this is technically not accurate since parameters are not copied when they are passed in; only the reference to the argument is copied. You can make Python simulate Call by Value by making a copy of the parameter when calling the function.)

```
```python
# Simulating call-by-value in Python

def foo(x):
    # Modify the passed-in object. The caller would normally see this
    # change, but if they called it with a copy, only the copy will
    # be affected.
    x[1] = 99

a = [1, 2, 3]

# Simulate call-by-value by making a copy
foo(a.copy())

print(a)  # [1, 2, 3]
```
```