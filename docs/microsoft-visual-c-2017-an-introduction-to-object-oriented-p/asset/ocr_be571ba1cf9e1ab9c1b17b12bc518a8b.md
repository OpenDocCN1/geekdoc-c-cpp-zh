# CHAPTER 12 Using Controls

Instead instantiating a named Font object, you can create and assign an anonymous Font in one step. In other words, an identifier is not provided for the Font, as in this example:

```
this.label1.Font = new
System.Drawing.Font("Courier New", 12.5F);
```

If you don't provide an identifier for a Font, you can reuse it, and you would have to create again to use it with additional Controls.

548

![](bbox=[0.161, 0.263, 0.876, 0.0033399999999999997])

+   1. You use the Font class to change the appearance of printed text on Controls in Forms.
2. When designing a Control on a Form, you must select a Font from the Properties list in the IDE.
3. The Font class includes several overloaded constructors.

> Properties list, but you also can create your own instance of the Font class. If you want to change the font, it is easiest to select a font from the default font. The false statement is #2. When designing a Control on a Form,

# Using a LinkLabel

A Link label is a control with a label that provides the user to link to other sources, such as Web pages or files. The C# class that creates a label is LinkLabel; it is a child of Label. Table 12-4 summarizes the properties and the default event method for LinkLabel. The default event for a Control is:

+   * The method whose is automatically created when you double-click the Control designing a project in the IDE
* The method that you are most likely to alter when use the Control
* The event that users most likely expect to generate when they encounter the Control in a working application

With many Controls, including a LinkLabel, a mouse click by the user triggers the default event. When designing a program, you can double-click a Control in the IDE to generate the default method shell, and write any necessary statements within the shell.

Copyright 2018 Cengage Learning. All Rights Reserved. May not be copied, scanned, or duplicated, in whole or in part. WCN 022-200-202