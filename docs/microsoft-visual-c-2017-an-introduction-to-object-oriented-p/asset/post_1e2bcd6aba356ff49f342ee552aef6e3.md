
# CHAPTER 3 Using GUI Objects and the Visual Studio IDE

(continued)

HelloWorld Microsoft Visual Studio Solution. Alternatively, select File from the menu, click Recent Projects and Solutions, and select the project from the pop-up list.

- 2. When the Form appears, drag a Label from the Toolbox to the Form. Change its Name to helloLabel and its Text property to Hello, Visual World! Change the Label's Location property to 80, 140.

- 3. Scroll through Properties list for helloLabel, and change its Visible property from True to False by clicking to the right of True, clicking the down arrow, and selecting False. You can still see helloLabel in the Designer, and the Label will be invisible when you execute the program.

- 4. Double-click the Button on the Form. A new window that contains program code is displayed, revealing a newly created displayButton_Click() method with no statements. Between the curly braces, type the following statement that causes the Label to appear when the user clicks the Button on the Form:

```
helloLabel.Visible = true;
```

- 5. Change the name of the displayButton_Click() method to use conventional Pascal casing by right-clicking the method name, Rename, and changing the highlighted name to start with an uppercase D. Click Apply.

- 6. Save the file, then run the program by clicking the menu bar and clicking Start Without Debugging, or by pressing Ctrl+F5. When the Form appears, click the Click here button to reveal the greeting. If you want, experiment with values for some of the Label properties, such as Font, BackColor, and ForeColor.

Adding Second Button to a Form

In the next steps, you add a Second Button to the Form in the HelloWorld project.

- 1. In the IDE, switch to Design View. Drag a second button onto the Form. Make its Location property 80, 195. Change the new Button's Name property to changeOutputButton and change its Text to Click me last. Drag the button's handles to adjust the size so that all text is visible.

- 2. Double-click the changeOutputButton to expose the changeOutputButton() method. Rename the method to use Pascal casing.

- 3. Between the curly braces of the method, add the following code:
```
helloLabel.Text = "Goodbye";
```

(continued)

(continued)

- 4. Save the project, execute the program. Click the displayOutputButton to reveal Hello, Visual World! Then click the changeOutputButton to reveal Goodbye.

- 5. Execute the program again. This time, click the second Button first. No message appears because the Label with the message has not been made visible. When you click the displayOutputButton, the Label becomes visible, but it displays Goodbye because the changeOutputButton's Click() method has already changed the Label's Text.

- 6. Return to the Form.cs [Design] tab. Click the changeOutputButton, change its Enabled property to False. Now, when the program executes, the user will not be able to click the second Button.

- 7. Double-click the displayOutputButton. Add the following statement to the Click() method so that the changeOutput becomes enabled when the displayOutputButton is clicked:

```
changeOutputButton.Enabled = true;
```

- 8. Save the project, execute the program. When the Form appears, the changeOutputButton is dimmed and not clickable because it is enabled. Click the enabled displayOutputButton to reveal the Hello, Visual World! message and enable the second Button. Then click the changeOutputButton to expose the Goodbye message.

- 9. Dismiss the Form, and close Visual Studio.

# Chapter Summary

- Forms GUI objects that provide an interface for collecting, displaying, and delivering information. They almost always include controls as labels, text boxes, and buttons that users can manipulate to interact with a program. Every Form and control on a Form has multiple properties you can use the IDE.

- The Toolbox displays a list of available controls you can add to a Form including controls such as Button, CheckBox, and Label. You can drag controls onto a Form. After you have dragged a Button to a Form, you can double-click to create the method that executes when a user clicks the Button, and you can write any statements between the curly braces of the Click() method.

# CHAPTER 3 Using GUI Objects and the Studio IDE

- Labels are controls that you use to display text to communicate with an application's user. TextBoxes are controls through which a user can enter data in a GUI application. Both have a Text property; frequently an application starts with the Text empty for TextBoxes. Because a user may enter any value, the TextBox is a string by default.

- Usually, you provide provable Name properties for all the controls you use on a Form. Although any identifier that starts with a letter is legal, by convention you should start control names with a lowercase letter and use camel case as appropriate, start Form names with an uppercase letter and use camel case as appropriate, and use the type of object in the name.

- If you build or run a program that has a syntax error, you see Build failed in the lower-left corner of the IDE and an error dialog box. An error list shows the line, position in the line, and project for each error. If you double-click an error message, the cursor is placed at the code where the error was found. If you inadvertently create an event-handling method that you do not want, you eliminate the event using the Properties window in the IDE. To remove an event method, you must refactor the code. Both console and GUI applications can contain variable declarations and similar statements. GUI applications use "snazzier," and they contain controls that a user can manipulate with mouse.

# Key Terms

The interface is the environment a program executes.

Forms are GUI objects that provide an interface for collecting, displaying, and delivering information.

Controls are devices such as labels, text boxes, and buttons that users can manipulate.

A node is an icon that appears a list or section of code and can be expanded or condensed.

An access specifier is a keyword that dictates whether outside classes use.

An event causes a program to perform a task.

A click event is the event generated when a user clicks a control.

A label is a control that you display text to communicate with an application's user.

A text box is a control through which a user can enter data in a GUI application.

Design time is the period during which a programmer designs the interface and writes the code.

Runtime is the period during which a program executes.

Focus describes the attribute of a Form control that stands out visually from the others and that reacts to keyboard input.

Tab order describes the sequence of controls selected when the user presses the Tab key.

A proportional font is one in which different characters have different pitches or widths.

A fixed-pitch monospaced font is one in which each character occupies the same width.

Code refactoring is the process of changing a program's internal structure without changing the way the program works.

An orphaned method is one that never executes in an application and thus serves no purpose.

# Review Questions

- 1. Which of the following is a GUI object that provides an interface for collecting, displaying, and delivering information that contains other controls?
  a. Button
  c. TextBox
  b. Form
  d. Label

- 2. In the Visual Studio IDE window, where does the menu bar lie?
  a. vertically along the left border
  b. vertically along the right border
  c. horizontally across the bottom of the window
  d. horizontally across the top

- 3. In the IDE, the area where you visually construct a Form is
  a. Toolbox
  c. Easel
  b. Form Designer
  d. Sandbox

- 4. When you create a new Windows Forms project, by default the First Form you is
  a. Form
  c. Form1
  b. FormA
  d. FormAlpha

- 5. The Form class has properties.
  a. three
  c. about 100
  b. ten
  d. about 100
