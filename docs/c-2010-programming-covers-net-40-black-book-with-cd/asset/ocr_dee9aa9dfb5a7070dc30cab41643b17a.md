+   - Hand — Shows an icon displaying a white X in a circle with a red background
+   - Information — Shows an icon displaying a lowercase letter i in a circle
+   - None — Does not show any icon
+   - Question — Shows an icon displaying a question mark in a circle
+   - Stop — Shows an icon displaying a white X in a circle with a red background
+   - Warning — Shows an icon displaying an exclamation mark in a triangle with a yellow background

The following are the values of the MessageBoxDefaultButton enumeration:

+   - Button1 — Makes the first button in the message box as the default button
+   - Button2 — Makes the second button in the message box as the default button
+   - Button3 — Makes the third button in the message box the as default button

The following are the values of the MessageBoxOptions enumeration:

+   - DefaultDesktopOnly — Displays the message box on the default desktop of Windows
+   - RightAlign — Displays the message box text as right-aligned.
+   - RtlReading — Specifies that the message box text is displayed in the right to left reading order
+   - ServiceNotification — Displays the message box on the active desktop when a service makes a call, notifying a user of an event

The result of the Show method is a value from the DialogResult enumeration. These values are: Abort, Cancel, Ignore, No, None, OK, Retry, and Yes.

Let’s create an application, MessageBoxMethod, to learn how to use the MessageBox.Show method to display a message box.

Perform the following steps to create the MessageBoxMethod application:

+   1. Create a Windows Forms application, named MessageBoxMethod.
+   2. Modify the Text property of Form1 to Message Displaying Form.
+   3. Add a Label (label1), TextBox (textBox1), and a Button (button1), to Form1.
+   4. Set the Text property of label1 to Message Text: (Figure 8.22).
+   5. Set the Text property of the button1 control to Click Me. Figure 8.22 shows the Design view of the MessageBoxMethod application:

![](bbox=[0.195, 0.58, 0.815, 0.882])

Figure 8.22: Displaying the Design View of the MessageBoxMethod Application