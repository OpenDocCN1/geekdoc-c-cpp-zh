+   18. If you are using the `MainMenu` object, to have the menu be displayed on the Form, you set the Menu property on the Form to the name of the `MainMenu` object.
+   19. There are a number of preconfigured dialog boxes that can be added to menus. They include those that resemble the standard Windows File Open, File Save, File Print, File Print Preview, Format Font, and Format Color dialog boxes. These can be added to your application by dragging and dropping the control object onto your form.
+   20. Check boxes appear as small boxes that allow users to make a Yes/No or True/False selection. The default event-handler method for CheckBox objects is `CheckedChanged()`. A `Click()` event can also be wired to CheckBox objects. Double-clicking on one of the CheckBox objects registers a `CheckedChanged()` event for that one object.
+   21. For visual appearances, CheckBox objects may be grouped together using the GroupBox control. The grouping also aids design because you can move all the objects as a group. However, grouping does not provide any additional functionality for CheckBox objects.
+   22. A GroupBox control should be placed on the form for radio buttons. Radio buttons give users a choice between two or more options. Remember that it is appropriate to select more than one CheckBox object. Not so with RadioButton objects.
+   23. Multiple radio buttons can be wired to the same event-handler method.
+   24. Windows Presentation Foundation (WPF) applications create a special XAML file with tags to control the appearance of an application. No .Designer.cs is created.
+   25. The `TabControl` object displays multiple tabs on the form, like labels in a set of folders in a filing cabinet. Each tab store different controls and has a `Click` event.

# EXERCISES

+   1. Delegates store:
+      a. the address for signatures of data
+      b. data and methods about the events in a program
+      c. events
+      d. the address of methods
+      e. all of the above