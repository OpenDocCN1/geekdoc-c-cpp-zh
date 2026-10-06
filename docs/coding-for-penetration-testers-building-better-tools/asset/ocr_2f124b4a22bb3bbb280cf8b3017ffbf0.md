the next. In this section, we will investigate the syntactical and conceptual differences in the concepts that have already been presented, and how they apply to the Python language.

# Getting Started

We want to create Python files in a text editor. Text editors are a matter of personal preference. As long as the indentation is consistent, Python won't mind. For those who do not already have an editor of choice, the gedit editor that was demonstrated in Chapter 1, Introduction to command shell scripting, has a graphical interface and is simple to use. In addition to having syntax highlighting, gedit handles automatic indentation, making it easier to avoid whitespace inconsistencies that could cause Python to fail.

Python scripts are .py files. For example, hello.py might be our first script. To use it, try typing gedit hello.py to create a simple script.

# Formatting Python files

Formatting is important in Python. The Python interpreter uses whitespace indentation to determine which pieces of code are grouped together in a special way—e.g., as part of a function, loop, or class. How much space is used is not typically important, as long as it is consistent. If two spaces are used to indent the first time, two spaces should be used to indent subently.

# Running Python files

Let's get comfortable with Python by writing a quick and simple script. Copy the following code into a text editor and save it as hello.py:

```
#!/usr/bin/python
user = "<your name>"
print "Hello " + user + "!"
```

Line one defines this as a Python script. This line is typically required for scripts written in Windows, but for cross-compatibility it is acceptable to include regardless of platform. It gives the path to