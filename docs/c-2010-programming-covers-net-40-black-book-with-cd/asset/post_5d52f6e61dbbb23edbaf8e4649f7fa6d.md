
Figure 8.56 shows the controls with modified properties:

![](img/e073a4882197be4ab61103cbe0bcb394_333_0.png)

Figure 8.56: Displaying Controls with Modified Properties

5. Add the code given in Listing 8.2 to the mouse and keyboard events of text boxes and button:

# Listing 8.2: Showing Mouse and Keyboard Events of Text Boxes and Button

```
private void textBox1_MouseEnter(object sender, EventArgs e)
{
    textBox1.BackColor = Color.Red;
    textBox1.ForeColor = Color.White;
}
private void textBox1_MouseLeave(object sender, EventArgs e)
{
    textBox1.BackColor = Color.White;
    textBox1.ForeColor = Color.Black;
}
private void textBox1_KeyPress(object sender, KeyPressEventArgs e)
{
    if (!Char.IsNumber(e.KeyChar))
    {
        MessageBox.Show("Enter only numbers.");
        textBox1.Text = "";
    }
}
private void textBox2_MouseEnter(object sender, EventArgs e)
{
    textBox2.BackColor = Color.Red;
    textBox2.ForeColor = Color.White;
}
private void textBox2_MouseLeave(object sender, EventArgs e)
{
    textBox2.BackColor = Color.White;
    textBox2.ForeColor = Color.Black;
}
private void textBox2_KeyPress(object sender, KeyPressEventArgs e)
{
    if (!Char.IsNumber(e.KeyChar))
    {
        MessageBox.Show("Enter only numbers.");
        textBox2.Text = "";
    }
}
private void button1_Click(object sender, EventArgs e)
{
    MessageBox.Show("The total is " + (Convert.ToInt32(textBox1.Text) + 
    Convert.ToInt32(textBox2.Text)));
}
```

6. Press the F5 key to execute the MouseandKeyboardEvents application. Figure 8.57 shows the output of the MouseandKeyboardEvents application:

![](img/e073a4882197be4ab61103cbe0bcb394_334_0.png)

# Figure 8.57: Displaying the Output of MouseandKeyboardEvents Application

When a user hovers the mouse over the Enter First Number text box, the background color of the text box changes to red, as shown in Figure 8.58:

![](img/e073a4882197be4ab61103cbe0bcb394_334_1.png)

# Figure 8.58: Demonstrating the MouseEnter Event

When you move away the mouse from the text box, the color of text box changes to white. Now, try entering alphabets in the text boxes. A message, Enter only numbers, is displayed in a message box, as shown in Figure 8.59:

![](img/e073a4882197be4ab61103cbe0bcb394_334_2.png)

# Figure 8.59: Displaying a Message Box

Now, when the user enters numbers in the text boxes and clicks the Add button, the sum of the entered numbers is displayed as a message, as shown in Figure 8.60:

![](img/e073a4882197be4ab61103cbe0bcb394_335_0.png)

Figure 8.60: Displaying the Sum of Two Numbers

You can find the code to handle keyboard and mouse events in the KeyboardandMouseEvent application available on the CD.

## Specifying Mouse Cursors for Windows Forms and Controls

You can use the Cursor property to set the mouse cursor type when the mouse moves over a control. As you know, a Windows Form is also derived from the Control class; therefore, cursor types are also applied to forms. You can set the Cursor property by specifying the values given in Table 8.11:

| Table 8.11: Mouse Cursor Options |
| Constant | Description |
| AppStarting | Specifies the combination of the Arrow cursor and the Wait cursor |
| Arrow | Specifies the Arrow cursor |
| Default | Specifies the Default cursor, usually an arrow cursor |
| Hand | Specifies the Hand cursor, usually used when hovering over a Web link |
| Help | Specifies the Help cursor, a combination of an arrow and a question mark |
| HSplit | Specifies the cursor that appears when the mouse is positioned over a horizontal splitter bar |
| IBeam | Specifies the I-beam cursor, which is used to show where the text cursor appears when the mouse is clicked |
| No | Specifies the cursor that indicates a particular region is invalid for the current operation |
| NoMove2D | Specifies the cursor for mouse wheel operations when the mouse is not moving; however, the window can be scrolled in either horizontal or vertical direction. |
| NoMoveHoriz | Specifies the cursor for mouse wheel operations when the mouse is not moving; however, the window can be scrolled in a horizontal direction |
| NoMoveVert | Specifies the cursor for mouse wheel operations when the mouse is not moving; however, the window can be scrolled in a vertical direction |
| PanEast | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in horizontal right direction |
| PanNE | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in north/east direction, which means either horizontal right or vertically upward direction |
| PanNorth | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling vertically in an upward direction |
| PanNW | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in north/west direction, which means horizontal left or vertically upward direction |
| PanSE | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in south/east direction, which means horizontal right or vertically downward direction |
| PanSouth | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling vertically in a downward direction |
| PanSW | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling in south/west direction, which means horizontal left or vertically downward direction |
| PanWest | Specifies the cursor for mouse wheel operations when the mouse is moving and the window is scrolling horizontally to the left |
| SizeAll | Specifies a four-headed cursor |
| SizeNESW | Specifies a two-headed diagonal (north/east and south/west) cursor |
| SizeNS | Specifies a two-headed vertical (north/south) cursor |
| SizeNWSE | Specifies a two-headed diagonal (northwest/southeast) cursor |
| SizeWE | Specifies a two-headed horizontal (west/east) cursor |
| UpArrow | Specifies the up-arrow cursor usually used to identify an insertion point |
| VSplit | Specifies the cursor that appears when the mouse is over a vertical splitter bar |
| WaitCursor | Specifies the Wait cursor, usually of an hourglass shape |

Figure 8.61 shows how to set the Cursor property of a control in the Properties window:

![](img/e073a4882197be4ab61103cbe0bcb394_336_0.png)

# Figure 8.61: Setting the Cursor Property in Properties Window

Now that you know about the various types of cursors that you can set for controls or forms, let's create an application named MouseCursorControl to set the cursor types for the controls, which are used in this application.

Perform the following steps to set the cursor types for controls:

- 1. Create a Windows Forms application, MouseCursorControl.
- 2. Add Button, TextBox, and CheckBox controls to Form1.
- 3. Set the Text property of Form1 to Mouse Cursor Form, as shown in Figure 8.62:

![](img/e073a4882197be4ab61103cbe0bcb394_337_0.png)

# Figure 8.62: Displaying Mouse Cursor Form

- 4. Add the following code snippet in the Load event of Form1 to set the Cursor property of various controls:

```
private void Form1_Load(object sender, EventArgs e)
{
    this.Cursor = Cursors.Help;
    button1.Cursor = Cursors.SizeAll;
    checkBox1.Cursor = Cursors.SizeNESW;
    listBox1.Cursor = Cursors.AppStarting;
}
```

5. Press the F5 key to execute the MouseCursorControl application. The Form1 form appears (Figure 8.63). Now, if you place the mouse pointer on the form, the pointer appears as the Help pointer type, as shown in Figure 8.63:

![](img/e073a4882197be4ab61103cbe0bcb394_337_1.png)

# Figure 8.63: Displaying Cursor Type for Form1

Similarly, the pointer type for the button control changes to the SizeAll cursor type, as shown in Figure 8.64:

![](img/e073a4882197be4ab61103cbe0bcb394_338_0.png)

Figure 8.64: Displaying Cursor Type for a Button Control

In case of Checkbox control, the mouse pointer changes to the SizeNESW cursor type on moving mouse over Mouse Cursor Form, as shown in Figure 8.65:

![](img/e073a4882197be4ab61103cbe0bcb394_338_1.png)

Figure 8.65: Displaying Cursor Type for a Checkbox Control

In case of Textbox control, the mouse pointer changes to the AppStarting cursor type on moving mouse over Mouse Cursor Form, as shown in Figure 8.66:

![](img/e073a4882197be4ab61103cbe0bcb394_338_2.png)

Figure 8.66: Displaying Cursor Type for a Textbox Control

You can find the code to specify the mouse cursor types for a form and its controls in the MouseCursorControl application available on the CD.

Now, let’s summarize the main topics discussed in this chapter.
