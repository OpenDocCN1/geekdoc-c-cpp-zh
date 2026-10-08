# # Errors

Sometimes programs don’t work the first time, but they can always be fixed. When code for a program isn’t entered correctly, Python will display an error message telling you what has gone wrong.

# ## Errors in the code window

When trying to run a program in the code window, you might see a pop-up window appear with an error message (such as "SyntaxError") in it. These errors stop the program from running and need to be fixed.

SEE ALSO
Bugs and 148-149 > debugging
What next? 176-177 >

+   1. Syntax error
If a pop-up window appears with a "SyntaxError" message, it often means there’s a spelling mistake or typing error in the code.

+   2. Error highlighted
Click "OK" in the pop-up window and you’ll go back to your program. There will be a red highlight on or near the error. Check that line matters carefully.

![](bbox=[0.0625, 0.513, 0.486, 0.903])

```
print('Hello World'!)
```

> There is a missing quote mark here
The error is highlighted

# ### EXPERT TIPS: classic errors

Some mistakes are particularly easy to make. Keep an eye out for these common problems:

+   **Upper vs lower case:** The case has to match exactly. If you write "Print" instead of "print", Python won’t understand the instruction.
**Single and double quotes:** Don’t mix up single and double quotes. All quotes needs a matching closing quote.
**Minus and underscore:** Underline can confuse the minus (-) with the underscore (_).
**Different brackets:** Different-shaped brackets, such as (), and [], are used for different things. Use the correct ones, and check there’s a complete pair.