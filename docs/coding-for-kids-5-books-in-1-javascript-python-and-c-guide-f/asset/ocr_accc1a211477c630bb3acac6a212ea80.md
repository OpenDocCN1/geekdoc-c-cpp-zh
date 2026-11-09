# Global and local Variables

Variables that are created outside functions are accessible to any function. They are called global functions. Global variables can be accessed by any function. Local variables are variables that are defined inside functions and cannot be accesses from outside function scopes.

In the code below “lang” variable is global so func() function can access it. When func() is called the output is python.

```
```python
# this variable is global to this scope
lang = "Python"

def func():
    print(lang)

func()
```
```

Python

```
```python
# this variable is global to this scope
lang = "Python"

def func():
    # this variable is local to this function
    lang = "C++"
    print(lang)

func()
print(lang)
```
```

C++

Python