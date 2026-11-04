6 Click the Events button in the Properties window, all the events related to text box are displayed in the Properties window (Fig.C#-5.26);

7 Double-click beside the KeyPress event to generate the textBox1_KeyPress event handler, as shown in Fig.C#-5.26;

![](bbox=[0.22, 0.21, 0.75, 0.4])

Fig.C#-5.26

8 Add the highlighted code in Code Editor, as given in Listing 5.4:

Listing 5.4: Showing the Code to Handle the KeyPress Event of the TextBox Control

```
private void textBox1_KeyPress(object sender, KeyPressEventArgs e)
{
    textBox1.BackColor = Color.Red;
    textBox1.ForeColor = Color.White;
}
```

9 Press the F5 key to run the KeyboardEvent application.
When you type some text in the TextBox control, the back color of the TextBox control changes to red and the text color changes to white, as shown in Fig.C#-5.27;

![](bbox=[0.35, 0.6, 0.6, 0.68])

Fig.C#-5.27

In this section, you learned about handling common events of a Windows Forms application. Now, let's learn to add controls to a form and perform certain operations on them.

# Working with Windows Forms Controls

Controls are components that can be placed on the form and used to display some information, accept some user input, and perform text editing. In addition, Windows controls are the basic controls that are used for creating applications in C# 2010. A control enhances user interaction with Windows Forms application. These controls are the common controls that are available in Toolbox of C# 2010. The common controls in Windows Forms application are as follows: