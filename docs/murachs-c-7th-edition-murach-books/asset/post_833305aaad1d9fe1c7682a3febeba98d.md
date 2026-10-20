
## The Invoice Total form

![](img/844f608d10a44654833ea5efc8a2e7a7_62_0.png)

### Description

- A text box is used to get the subtotal from the user. Read-only text boxes are used to display the discount percent, discount amount, and total. And label controls are used to identify the values that are in the text boxes on the form.
- After entering a subtotal, the user can click the Calculate button to calculate the discount percent, discount amount, and total. Alternatively, the user can press the Enter key to perform the calculation.
- To calculate another invoice total, the user can enter another subtotal and then click the Calculate button or press the Enter key again.
- To close the form and end the application, the user can click the Close button in the upper right corner of the form or click the Exit button. Alternatively, the user can press the Esc key to exit from the form.
- The user can press Alt+C to activate the Calculate button or Alt+X to activate the Exit button. On most systems, the letters that activate these buttons aren’t underlined until the user presses the Alt key.

### Three types of controls

- A label displays text on a form.
- A text box lets the user enter text on a form.
- A button initiates form processing when clicked.

## How to add controls to a form

Figure 2-4 shows how you can use the Toolbox to add controls to a form. The easiest way to do that is to click on the control in the Toolbox, then click the form at the location where you want to add the control. In this figure, for example, the button control is selected in the Toolbox, and the mouse pointer is positioned over the form.

Once you add a control to a form, you can resize the control by selecting it and dragging one of its handles, and you can move the control by dragging the control to a new location on the form. If you prefer, you can place and size the control in a single operation by clicking the control in the Toolbox, then clicking and dragging in the form.

A second way to add a control is to drag the control from the Toolbox to the form. The control is placed wherever you drop it. You can then resize the control.

A third method for adding controls is to double-click the control you want to add in the Toolbox. This places the control in the upper left corner of the form. You can then move and resize the control.

If the AutoHide feature is activated for the Toolbox and you click on the Toolbox tab to display it, the display frequently obscures some or all of the form. This makes it difficult to add controls. As a result, it’s a good idea to turn off the AutoHide feature when you’re adding controls. To do that, just click the pushpin button in the upper right corner of the Toolbox.

After you have added controls to the form, you can work with several controls at once. For example, let’s say that you have four text box controls on your form and you want to make them all the same size with the same alignment. To do that, first select all four controls by holding down the Ctrl or Shift key as you click on them or by using the mouse pointer to drag a dotted rectangular line around the controls. Then, use the commands in the Format menu or the buttons in the Layout toolbar to move, size, and align the controls relative to the primary control. If you select the controls one at a time, the primary control will be the first control you select. If you select the controls by dragging around them, the primary control will be the last control in the group. To change the primary control, just click on it. (The primary control will have different color handles so you can identify it.)

Although these techniques may be hard to visualize as you read about them, you’ll find that they’re relatively easy to use. All you need is a little practice, which you’ll get in the exercise for this chapter.

### A form after some controls have been added to it

![](img/844f608d10a44654833ea5efc8a2e7a7_64_0.png)

### Three ways to add a control to a form

- Select the control in the Toolbox. Then, click in the form where you want to place the control. Or, drag the pointer on the form to place and size the control.
- Double-click the control in the Toolbox. Then, the control is placed in the upper left corner of the form.
- Drag the control from the Toolbox and drop it on the form. Then, the control is placed wherever you drop it.

## How to select and work with controls

- To select a control on the form, click it.
- To move a control, drag it.
- To size a selected control, drag one of its handles. Note, however, that a label is sized automatically based on the amount of text that it contains. As a result, you can’t size a label by dragging its handles unless you change its AutoSize property to False.
- To select more than one control, hold down the Shift or Ctrl key as you click on each control. You can also select a group of controls by clicking on a blank spot in the form and then dragging around the controls.
- To align, size, or space a group of selected controls, click on a control to make it the primary control. Then, use the commands in the Format menu or the buttons on the Layout toolbar to align, size, or space the controls relative to the primary control.
- You can also size all of the controls in a group by sizing the primary control in the group. And you can drag any of the selected controls to move all the controls.
- To change the size of a form, click the form and drag one of its sizing handles.

## A form after the properties have been set

![](img/844f608d10a44654833ea5efc8a2e7a7_66_0.png)

### Description

- The Properties window displays the *properties* for the object that’s currently selected in the Form Designer window. To display the properties for another object, click on that object or select the object from the drop-down list at the top of the Properties window.
- To change a property, enter a value into the text box or select a value from its drop-down list if it has one. If a button with an ellipsis (...) appears at the right side of a property’s text box, you can click on the ellipsis to display a dialog box that lets you set options for the property.
- To change the properties for two or more controls at the same time, select the controls. Then, the common properties of the controls are displayed in the Properties window.
- When you click on a property in the Properties window, a brief explanation of the property appears in a pane at the bottom of the window. For more information, press F1 to display the help information for the property.
- You can use the first two buttons at the top of the Properties window to sort the properties by category or alphabetically.
- You can use the plus (+) and minus (-) signs displayed to the left of some of the properties and categories in the Properties window to expand and collapse the list of properties.

### Note

- If a description isn’t displayed when you click on a property in the Properties window, right-click on the window and select Description from the shortcut menu.

## Common properties for forms and controls

Figure 2-6 shows some common properties for forms and controls. The first two properties apply to both forms and controls. The other properties are presented in two groups: properties that apply to forms and properties that apply to controls. Note that some of the control properties only apply to certain types of controls. That’s because different types of controls have different properties.

Since all forms and controls must have a Name property, Visual Studio creates generic names for all forms and controls, such as Form1 or button1. Often, though, you should change these generic names to something more meaningful, especially if you’re going to refer to them in your C# code.

To make your program’s code easier to read and understand, you can begin each name with a two- or three-letter prefix in lowercase letters to identify the control’s type. Then, you can complete the name by describing the function of the control. For instance, you can use a name like btnExit for the Exit button and txtSubtotal for the Subtotal text box.

For Label controls, you can leave the generic names unchanged unless you plan on modifying the properties of the labels in your code. For example, if you want to use a label control to display a message to the user, you can give that label a meaningful name such as lblMessage. But there’s no reason to change the names for label controls that display text that won’t be changed by the program.

Forms and most controls also have a Text property that is visible when the form is displayed. A form’s Text property is displayed in the form’s title bar. For a control, the Text property is usually displayed somewhere within the control. The Text property of a button, for example, is displayed on the button, and the Text property of a text box is displayed in the text box.

As you work with properties, you’ll find that you can set some of them by selecting a value from a drop-down list. For example, you can select a True or False value for the TabStop property of a control. For other properties, you have to enter a number or text value. And for some properties, a button with an ellipsis (...) is displayed. Then, when you click this button, a dialog box appears that lets you set the property.
