shows an input dialog or an internal input dialog. (An internal dialog is rendered entirely within its owner’s frame.) Returns the input string typed by the user, or `null` if the user canceled the dialog. The parent component can be `null`. The message to show on the dialog can be a string, icon, component, or an array of them. The `messageType` parameter is one of `ERROR_MESSAGE`, `INFORMATION_MESSAGE`, `WARNING_MESSAGE`, `QUESTION_MESSAGE`, `PLAIN_MESSAGE`.

# 11.7.2 Creating Dialogs

In the last section, you saw how to use the `JOptionPane` class to show a simple dialog. In this section, you will see how to create such a dialog by hand.

[Figure 11.31](#figure-11-31) shows a typical modal dialog box—a program information box that is displayed when the user clicks the About button.

![](bbox=[0.272, 0.498, 0.729, 0.733])

**Figure 11.31** An About dialog box

To implement a dialog box, you extend the `JDialog` class. This is essentially the same process as extending `JFrame` for the main window for an application. More precisely: