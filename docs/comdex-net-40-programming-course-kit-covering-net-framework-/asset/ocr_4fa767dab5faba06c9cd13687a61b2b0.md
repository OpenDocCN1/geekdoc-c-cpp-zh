+   8. Change the Text property of the first and second Label controls to Enter the First Character of Name: and Result, respectively, and the Text property of the Button control to Click, as shown inFig.C#.6.48:

![](bbox=[0.15, 0.12, 0.85, 0.4])

+   9. Double-click the Click button and add the highlighted code, given in Listing 6.21, in the Code Editor.
+   
+   Listing 6.21: Showing the Code for the Click Event of the Button1 Control

```
```csharp
private void button1_Click(object sender, EventArgs e)
{
    textBox2.Text = "";
    string[] arrNames = { "Avantika", "Priya", "Ira", "Jaya",
                          "Amrita", "Puja" };
    foreach (var Name in arrNames.Where(n)
        => n.StartsWith(textBox1.Text)))
    {
        textBox2.Text = (textBox2.Text + Name) + ",";
    }
}
```
```

In Listing 6.21, a string array, arrNames, is defined and some names are added to it. We have also created a Lambda expression in the foreach loop, which displays all the names in textBox2 that begin with the text, entered in textBox1.

+   10. Press the F5 key on the keyboard to execute the LambdaExpression application and enter some text in textBox1. In our case, we have entered the letter A in textBox1, as shown in Fig.C#.6.49:

![](bbox=[0.2, 0.83, 0.7, 0.95])

+   11. Click the Click button. The names that start with the alphabet entered in textBox1 are displayed in textBox2, as shown in Fig.C#.6.50: