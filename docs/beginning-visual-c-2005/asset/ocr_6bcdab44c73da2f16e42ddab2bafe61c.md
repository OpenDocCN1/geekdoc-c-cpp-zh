Here you create an array of integer values the same length as the array of button handles that is passed as the argument. You then populate the values array with the int equivalents of the string returned by the Text properties of the buttons, and return the handle to the values array.

After compiling the project once more, you should have a fully functional application. You can generate lottery entries for a variety of lotteries with the range of values constrained or not. You can also elect to generate new random individual values in an entry or choose your own. It has always worked but never won for me; of course, working is a measure of success.

# Summary

In this chapter, you assembled a Windows Form application that uses the controls that you are most likely to need in the majority of programs. It should be apparent that Windows Forms programs are geared exclusively to using the Design capability. All the code for a class goes into the class definition, so with a very complex form the class is many lines of code. With a production application the code consists of a number of large classes that are rather unstructured, and difficult to modify and maintain at the code level. You should therefore always use the Design capability and the Properties window to expedite changes wherever you can and whenever you need to access the code, use Class View to find your way around.

The key points to keep in mind from this chapter include:

+   - An application window is a form, and a form is defined by a class derived from the System::Form class.
+   - A dialog window is a form that has its FormBorderStyle property value set to FixedDialog.
+   - A dialog box can be created as a modal dialog by calling its ShowDialog() function or as a modeless dialog by calling its Show() function.
+   - You can control whether or not a dialog box closes by setting the DialogResult property value for the dialog object.
+   - A ComboBox control combines the capabilities of a ListBox and a TextBox and allows selection of an item from a list or a new item to be entered from the keyboard.
+   - A NumericUpDown control allows the entry of numeric data by stepping through values within a given range with a given step increment.
+   - You can add the definition of a Click event handler for a control by double-clicking the control in the Form Design tab.
+   - You can specify an existing function to be a handler for a given event for a control through the Properties window. Clicking the Events button in the Properties window displays the list of events for a control.
+   - You should only change the names of automatically generated class members through the Properties window — not directly using the Code editor.