5. Press the F5 key to run and execute the application. As a result, Form1 appears, as shown in Figure 8.49:

![](bbox=[0.35, 0.105, 0.67, 0.315])

Figure 8.49: Displaying the Output of AccessCharacters Application

Form1 displays the button control having the caption Print, with the first character P of Print underlined. Now, Press the Alt+P key combination on the keyboard to display a message box, as shown in Figure 8.50:

![](bbox=[0.4, 0.375, 0.63, 0.485])

Figure 8.50: Displaying a Message Box by Using an Access Character

You can also click the Print button to display the message box, which is shown in Figure 8.50. The Alt+P key combination is the shortcut of the Print button with the specified character, P. In the same way, you can create access characters for a variety of commands. You can find the code to specify access characters for the Button control in the AccessCharacters application available on the CD.

# Moving and Resizing Controls

In C# 2010, you can use the SetBounds method to move forms and controls. The Size and Location properties are used to set dimensions of forms and controls. These properties are specified by the Size and Point classes, respectively. The objects of these classes are created by passing the values to the x and y dimensions in their class's constructors, Size(x_dimension, y_dimension) and Point(x_location, y_location), respectively. The dimensions you set in Size and Point objects are measured in pixels. In the coordinate system of a Windows Form, the upper left of the form is the origin (0, 0), where positive x values increase downwards, and positive y values increase to the right.

Let's perform the following steps to learn how to move and resize the controls:

+   1. Create a Windows Forms application named MoveResizeControls.
+   2. Add a Button control, button1, to Form1.
+   3. Modify the Text property of Form1 to Move and Resize Form.
+   4. Add the following code snippet in the Click event of button1:

```
private void button1_Click(object sender, EventArgs e)
{
    Size = new Size(100, 100);
    Location = new Point(0, 0);
    button1.Size = new Size(100, 50);
    button1.Location = new Point(0, 0);
}
```

5. Press the F5 key to run and execute the application. As a result, Form1 appears, as shown in Figure 8.51: