+   10. *Double-click* the Form1 form and type the code snippet, given in Listing 7.5, in its Load event:

# **Listing 7.5:** Adding the Code in the Load Event of Form1

```
```csharp
private void Form1_Load(object sender, EventArgs e) {
    string str1, str2;
    str1 = "welcome to ";
    str2 = "C# 2010";
    label1.Text = str1 + str1;
}
```
```

In Listing 7.5, two variables of the string data type, **str1** and **str2**, have been assigned the values **Welcome to** and **C# 2010**, respectively. Finally, the concatenated values of the both variables str1 and str2 are displayed on a label.

+   11. *Press* the F5 key to execute the application. The form appears, as shown in Fig.C#-7.15:

![](bbox=[0.422, 0.308, 0.601, 0.446])

Fig.C#-7.15

As shown in Fig.C#-7.15, the message displayed on the label is **Welcome to Welcome to**; whereas, you expected the message **Welcome to C# 2010**. To determine why the expected output does not appear, you need to check the string concatenating statement by inserting a breakpoint in the code. A **breakpoint** suspends the execution of a program at a certain point. At this point of time, your program is said to be in the break mode. The execution can be resumed at any time.

+   12. *Find* the statement **label1.Text = str1 + str1**, and then *click* the left-hand margin next to that statement to set a breakpoint, as shown in Fig.C#-7.16:

![](bbox=[0.305, 0.573, 0.72, 0.81])

Fig.C#-7.16

A red dot appears on the left-hand margin and the entire statement is highlighted with red color, when a breakpoint is set, as shown in Fig.C#-7.17: