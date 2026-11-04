> NOTE The Locals window is similar to the Watch window except it shows the values of all of the local variables (and constants). This window is handy if you want to view many of those variables all at once. It also highlights recently changed values in red so you can see what's changing.

# USING THE IMMEDIATE WINDOW

While the program is stopped, the Immediate window lets you execute simple commands. The four most useful commands that this window supports let you view variable values, evaluate expressions, set variable values, and call methods.

> NOTE If you can't find the Immediate window, open the Debug menu, expand the Windows submenu, and select Immediate.

To view a variable's value, simply type the variable's name and press Enter. (Optionally, you can type a question mark in front if it makes you feel more like you're asking a question.)

The following text shows the Immediate window after I typed in the name of the variable subtotal and pressed Enter:

```
subtotal
19.95
```

To evaluate an expression, simply type in the expression and press Enter. You can include literal values, variables, properties, constants, and just about anything else that you can normally include inside an expression in the code.

The following text shows the Immediate window after I typed an expression and pressed Enter:

```
taxRate * subtotal
179.55
```

To set a variable's value, simply type the variable's name, an equals sign, and the value that you want to give it. The new value can be a literal value or it can be the result of an expression. After you press Enter, the Immediate window evaluates whatever is on the right of the equals sign, saves it in the variable, and then displays the variable's new value.

> NOTE The same technique lets you set new values for properties. For example, you can change a control's Location, Text, Visible, BackColor, and other properties on the fly.