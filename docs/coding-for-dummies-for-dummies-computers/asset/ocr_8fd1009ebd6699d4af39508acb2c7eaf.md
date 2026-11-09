![](bbox=[0.23, 0.135, 0.638, 0.326])

Figure 14-1: An `if-else` statement with an `elif`.

Imagine the user entered his name, “Jeff Bezos.” You can display the value of the variable using `print(full_name)` and you would see this

```
Jeff Bezos
```

Python, unlike Ruby, does not store the newline `\n` escape sequence after user input.

At this point, you may feel like printing variables and values in a Python interpreter console window is very different from dynamically creating web pages with variables created in Python. Integrating Python into a web page to respond to user requests and generate HTML pages is typically done with a Python web framework, like Django or Flask, which have pre-written code to make the process easier. These frameworks typically require some installation and set-up work, and generally separate the data being displayed from templates used to display the page to the user.

![](bbox=[0.132, 0.447, 0.21, 0.52])

# Shaping Your Strings

Whenever you collect input from users, you need to clean the input to remove errors and inconsistencies. Here are some common data cleaning tasks:

+   - Standardizing strings to have consistent upper and lower case
+   - Removing white space from user input
+   - Inserting a variable’s value in strings displayed to the user

Python includes many built-in methods that make processing strings easy.