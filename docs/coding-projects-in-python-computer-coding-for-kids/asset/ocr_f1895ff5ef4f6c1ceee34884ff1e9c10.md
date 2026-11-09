# Using a module

To use a module in your code, you have to tell Python that you would like to include it. You instruct Python which modules to include using import statements. There are a few different ways that you can do this, depending on what you need from the module.

![](bbox=[0.608, 0.088, 0.926, 0.233])

# ▷ import...

Typing the keyword import allows you to use all the contents of a module. However, you need to put the module’s name before any function you use. This code imports all the webbrowser module and uses its open() function to open the Python website in the computer’s browser.

```
>>> import webbrowser
>>> webbrowser.open('https://docs.python.org/3/library/')
```

This line imports the whole webbrowser module.

The name of the module comes before the function.

# ▷ from... import...

If you only want to use a particular part of a module, you can import just that part by adding the from keyword. Now you can just use the function on its own. This code imports the random module’s choice() function. The function picks a random item from any list you give it.

```
>>> from random import choice
>>> direction = choice(['N', 'S', 'E', 'W'])
>>> print(direction)
W
```

Only the choice function is imported from the random module.

No module name is needed.

The code prints a random direction.

# ▷ from... import... as...

Sometimes you may want to change the name of an imported module or function, perhaps because you’ve already used that name or maybe it isn’t clear enough. To do this, use the keyword as followed by the new name. In the example shown here, the time() function, which we’ve renamed time_now(), gives us the current time. The time given is the exact number of seconds since 00:00 on January 1, 1970—a date used by most computers as the start of their clock.

```
>>> from time import time as time_now
>>> now = time_now()
>>> print(now)
1478092571.003539
```

This line imports and renames the time() function.

This variable uses the function’s new name.

The number of seconds since 00:00 on January 1, 1970

![](bbox=[0.429, 0.851, 0.95, 0.999])