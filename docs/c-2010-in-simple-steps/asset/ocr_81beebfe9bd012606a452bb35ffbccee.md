![](bbox=[0.405, 0.15, 0.595, 0.295])

In Fig.C#5.36, the fore color of the label is changed to blue when the Blue radio button is selected.

# Using the CheckBox Control

A CheckBox control accepts a value of either true or false. You need to just click the CheckBox control to select it. When the CheckBox control is selected a check mark appears; click the control again to deselect it. When you select the CheckBox control, it holds the value, true and when you deselect the CheckBox control, it holds the value, false. A CheckBox control can display an image or corresponding text associated with it. It can also display both at the same time.

Let's perform the following steps to use the CheckBox control in the ControlApplication application:

+   1. Drag two CheckBox controls from Toolbox and drop it on the Form1 form (Fig.C#5.37).
+   2. Set the Text property of checkBox1 to Bold in the Properties window, as shown in Fig.C#5.37:
+   3. Change the Text property of checkBox2 to Italic in the Properties window.
+   4. Double-click the check box, Bold and add the highlighted code shown in Listing 5.10 on the CheckedChanged event of checkBox1:

![](bbox=[0.385, 0.495, 0.595, 0.615])

# Listing 5.10: Adding Code on the CheckedChanged Event of checkBox1

```
private void checkBox1_CheckedChanged(object sender, EventArgs e)
{
    label1.Font = new Font(label1.Font.Name, label1.Font.Size, label1.Font.Style |
    FontStyle.Bold);
}
```

In Listing 5.10, the code changes the font of the text displayed on the label1 label to bold when you select the Bold check box.

5 Add the highlighted code shown in Listing 5.11 on the CheckedChanged event of checkBox2:

# Listing 5.11: Adding Code on the CheckedChanged Event of checkBox2

```
private void checkBox2_CheckedChanged(object sender, EventArgs e)
{
```