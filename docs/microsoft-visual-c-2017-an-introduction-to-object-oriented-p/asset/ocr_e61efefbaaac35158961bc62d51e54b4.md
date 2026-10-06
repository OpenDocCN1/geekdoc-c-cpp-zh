# CHAPTER 3 Using GUI Objects and the Visual Studio IDE

![](bbox=[0.298, 0.065, 0.863, 0.417])

Label dragged onto
Form1 from Toolbox

![](bbox=[0.173, 0.303, 0.263, 0.335])

Text property of
label1 changed

Figure 3-7 A Label on a Form

string of text; depending on the amount of text you enter, you might need to change the size of
the Label by dragging its handles or resizing its Size property.

In 3-7, Enter a number has been assigned to label1’s Text property. If you want to
create multiple lines of text, click the small, downward-pointing arrow to the right
the Text property value to open an editor, and type the needed text in separate lines.
y might want a program to start with no text appearing on a label. If so, delete the entry from
the Text property in the Properties list. If you make any changes to its color, the label will be invisible to the user. Note that a label’s
Text property can be blank, but a Label’s Name property cannot.

A text box is a GUI control through which a user can enter data; the C# class is TextBox.
Figure 3-8 shows a TextBox on a Form. If the intention is to enter data in a TextBox,
you might want to start with its Text empty, but you are allowed to add text to it
Text property if desired.

Figure 3-9 shows a Form with three Labels, two TextBoxes, and a Button. The first Label
has not yet been provided with new text, so it still contains label3. You can delete the
value in the Properties window if you want the Label1 to be empty at first.

When you run the program that displays the Form in Figure 3-9, the intention is for
tuser to enter a number in each TextBox. When the user clicks the Button, the sum of the
two numbers will be displayed in label13. To sum them, you must write code for the
Button. In the Form Designer, double-click to expose the prewritten shell
of the button1_Click() method.

Figure 3-10 shows the code you can write inside button1_Click() method. The method
contains declarations for three integers. When a user types a value into a TextBox in executing