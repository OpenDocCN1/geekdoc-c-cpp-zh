![](bbox=[0.305, 0.136, 0.778, 0.4])

Fig.C#-7.17

+   13. Press the F5 key to restart the execution of the application.
+   
+   Observe that now the application is suspended for a while and the line with the break point is highlighted with the yellow color. Now, verify the values of the variables using Immediate Window. You can observe that instead of concatenating `str1` and `str2` variables, you have concatenated `str1` and `str1` variables. Therefore, the message box is displaying the message **Welcome to Welcome to**.

+   14. Press the SHIFT + F5 keys together to stop the debugging of the application and remove the breakpoint by clicking the red dot again on the left-hand margin of Code Editor.

+   15. Rectify the logical error by replacing the code in the Load event of Form1 with the code snippet given in Listing 7.6:

# Listing 7.6: Rectifying the Logical Error

```
```csharp
private void Form1_Load(object sender, EventArgs e)
{
    string str1, str2;
    str1 = "Welcome to ";
    str2 = "C# 2010";
    label1.Text = str1 + str2;
}
```
```

In Listing 7.6, the **str1** and **str2** variables are concatenated and the result is shown on the label.

+   16. Press the F5 key to execute the application. The output is now displayed, as shown in Fig.C#-7.18:

![](bbox=[0.422, 0.71, 0.601, 0.849])

Fig.C#-7.18