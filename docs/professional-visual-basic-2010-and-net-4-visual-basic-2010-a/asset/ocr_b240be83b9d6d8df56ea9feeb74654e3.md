# Form Borders

Forms have a number of border options in Windows Forms. The FormBorderStyle property is used to set the border option, and the options can affect the way a form can be manipulated by the user. The options available for FormBorderStyle include the following:

+   - None — No border, and the user cannot resize the form
+   - FixedSingle — Single 3-D border, and the user cannot resize the form
+   - Fixed3D — 3-D border, and the user cannot resize the form
+   - FixedDialog — Dialog-box-style border, and the user cannot resize the form
+   - Sizeable — Same as FixedSingle, except that the user can resize the form
+   - FixedToolWindow — Single border, and the user cannot resize the form
+   - SizeableToolWindow — Single border, and the user can resize the form

Each of these has a different effect on the buttons that appear in the title bar of the form. For details, check the help topic for the FormBorderStyle property.

# Always on Top — the TopMost Property

Some forms need to remain visible at all times, even when they don’t have the focus, such as floating toolbars and tutorial windows. In Windows Forms, forms have a property called TopMost. Set it to True to have a form overlay other forms even when it does not have the focus.

Note that a form with TopMost set to True is on top of all applications, not just the hosting application. If you need a form to only be on top of other forms in the application, then this capability is provided by an owned form.

# Owned Forms

As with the TopMost property, an owned form floats above the application but it does not interfere with using the application. An example is a search-and-replace box. However, an owned form is not on top of all forms, just the form that is its owner.

When a form is owned by another form, it is minimized and closed with the owner form. Owned forms are never displayed behind their owner form, but they do not prevent their owner form from gaining the focus and being used. However, if you want to click on the area covered by an owned form, the owned form has to be moved out of the way first.

A form can only have one “owner” at a time. If a form that is already owned by Form1 is added to the owned forms collection for Form2, then the form is no longer owned by Form1.

There are two ways to make a form owned by another form. It can be done in the owner form or in the owned form.

# AddOwnedForm Method

In the owner form, another form can be made owned with the AddOwnedForm method. The following code makes an instance of Form2 become owned by Form1. This code would reside somewhere in Form1 and would typically be placed just before the line that shows the instance of Form2 to the screen:

```
Dim frm As New Form2
Me.AddOwnedForm(frm)
```

# Owner Property

The relationship can also be set up in the owned form. This is done with the Owner property of the form. Here is a method that would work inside Form2 to make it owned by a form that is passed in as an argument to the function: