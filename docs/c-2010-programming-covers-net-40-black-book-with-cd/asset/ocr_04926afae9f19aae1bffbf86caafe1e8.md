```
private void Form1_Activated(object sender, EventArgs e)
{
    textBox2.Focus();
}
```

In the preceding code snippet, we have set the focus of textBox2 of the Form1 form.

Now, press the F5 key to execute the application. The focus of the cursor appears on the second text box (that is, textBox2), as shown in Figure 8.44:

![](bbox=[0.32, 0.185, 0.7, 0.435])

Figure 8.44: Showing the Focus on a Textbox Control

You can find the code of the SetFocus application on the CD.

# Specifying the Tab Order of Controls

In general, you use a mouse to perform actions, such as selecting, deselecting, and scrolling. However, suppose your mouse is not working and you still want to access the application. In that case, you try to access the application through your keyboard by using the Tab key. This is possible only if you have set the correct tab order using the Properties window of a form. You can navigate from one control to another by using the Tab key from the keyboard. You can set the tab order of controls as per your requirement. To set the tab order of controls, you need to set the TabStop property of the selected control to True and specify the value in the TabIndex property to set the control’s position in the tab order, as shown in Figure 8.45:

![](bbox=[0.32, 0.63, 0.735, 0.88])

Figure 8.45: Displaying the TabIndex and TabStop Properties