# Errors in the shell window

Sometimes, an error message will appear in red text in the shell window. This will also stop the program from working.

# Name error

If the error message "NameError" appears, it means Python can't understand one of the words that has been used. If the error is in code in the code window, right-click on the error message in the shell window and select "Go to file/line"

![](bbox=[0.605, 0.08, 0.953, 0.215])

The line in the code (in the code window) where the error was found

Traceback (most recent call last):

```
File "C:\PythonCode\errors.py", line 1, in <module>
pront('Hello World!')
```

NameError: name 'pront' is not defined

| Cut |
| Copy |
| Paste |
| Go to file/line |

The word Python doesn't understand

Click to highlight the line where the error appears in the code window

# Fix the error

The line with the error is highlighted in the code window. The word "pront" has been typed instead of "print". You can edit the code to fix the error.

```
pront('Hello World!')
```

Change this to read "pront"

# Spotting errors

Use the tips on these two pages to find the line in the code where the errors appear, double-check that line. Go through the checklist on the right to find out what has gone wrong.

| Check your code for the following points |
| Have you copied exactly what you were asked to enter? |
| Have you spelled everything correctly? |
| Are there two quote marks ('\') around the expression you want to print? |
| Do you have extra spaces at the beginning of the line? Spacing is very important in Python. |
| Have you checked the lines above and the highlighted line? Sometimes that's where the problem is. |
| Have you asked someone else to check the code against the book? They might spot something you have missed. |
| Are you using Python 3 not Python 2? Programs for 3 don't always work in Python 2. |

![](bbox=[0.068, 0.773, 0.473, 0.953])

There are some methods you can use to find errors more easily. A handy checklist.