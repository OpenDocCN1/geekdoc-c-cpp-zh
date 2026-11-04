![](bbox=[0.24, 0.15, 0.78, 0.34])

6 Double-click the Button control and add the highlighted code given in Listing 5.3 in Code Editor, to handle the Click event of the Button control:

Listing 5.3: Showing the Code to Handle the Click Event of the Button Control

```
private void button1_Click(object sender, EventArgs e)
{
    textBox1.Text = "Welcome to C# 2010";
}
```

7 Press the F5 key to run the MouseEvent application. The output after clicking the Click button is shown in Fig.C# 5.25:

![](bbox=[0.38, 0.49, 0.6, 0.62])

In Fig.C# 5.25, the text Welcome to C# 2010 is displayed in text box.

Now, let's learn to handle keyboard events.

# Handling Keyboard Events

In C#, along with mouse events, you can also generate keyboard events. The different keyboard events in Windows Forms application are KeyDown, KeyPress, and KeyUp.

Let's learn to handle the KeyPress event of a TextBox control by performing the following steps:

+   1. Repeat steps 1-3 of the Changing the Title of a Form section of this chapter.
+   2. Enter KeyboardEvent in the Name text box and specify an appropriate location in the Location combo box.
+   3. Click the OK button. The KeyboardEvent application is created with the specified name and location.
+   4. Drag a TextBox control from Toolbox and drop it on the Form1 form (Fig.C# 5.26).
+   5. Select the text box control you just added and open the Properties window to handle the KeyPress event of the TextBox control (Fig.C# 5.26).