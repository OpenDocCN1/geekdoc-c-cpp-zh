# EXERCISES

+   1. Build the UserForms application shown in Figure 9-3.
+   2. [WPF] Repeat Exercise 1 with a WPF application. (Hint: Don't forget to make all of the forms close when you close the main window.)
+   3. Build the RemoteForm application shown in Figure 9-4.
+   4. [WPF] Repeat Exercise 3 with a WPF application. Hints:
+      - In WPF, set colors equal to brushes as in Brushes.Red.
+      - To set the remote window's background color, set its Background property.
+      - To set the remote form's text color, set the Label's Foreground property.
+      - You don't need to set the Modifiers property in WPF. (WPF controls don't have that property.)
+   5. Modify the program you wrote for Exercise 3 so the buttons also change the label on the color form. For example, the Red button should make the label say, "I'm red!" (Hint: Don't forget to set the Label's Modifiers property to Public.)
+   6. [WPF] Repeat Exercise 5 with the WPF application you built for Exercise 4.
+   7. [WPF] Repeat the Try It with a WPF application. (Hint: Don't forget to set the ShowInTaskbar property.)
+   8. Unfortunately The Try It has a major problem. If you close one of the secondary forms and then click the main form's button to redisplay that form, the program crashes.
+      When you close the form, it is destroyed. When you click the button again, the program tries to display the destroyed form and that won't work.
+      To fix the program, give each of the secondary forms a FormClosing event handler similar to the following:
+      The first statement cancels the close so the form stays open. The second statement makes the form invisible but keeps it alive.
+   9. [WPF] Repeat Exercise 8 for the WPF program you built in Exercise 7. (Hint: In WPF you need to use the Closing event.)
+   10. Make a program that displays a Button that says "New Form." When the user clicks the Button, display a new non-modal instance of the same kind of form. (What happens when you click the new form's button? What happens if you close the new form? What happens if you make several forms and then close the original one?)

```
private void LodgingForm_FormClosing(object sender,
    FormClosingEventArgs e)
{
    e.Cancel = true;
    Hide();
}
```