+   9. *Drag and drop* the controls, listed in Table 7.3, onto the Form1 form and also set the values for their properties:

| Controls | Name Property Value | Text Property Value |
|---|---|---|
| Label | label1 | Enter No. (0-10) |
| TextBox | textBox1 | [Blank] |
| Button | button1 | Submit |

+   10. *Double-click* the **Submit** button and add the code snippet, given in Listing 7.8, in the *Click* event of the button:

# Listing 7.8: Showing the Code to Throw an Exception Using the throw Statement

```
private void button1_Click(object sender, EventArgs e)
{
    int num1 = 0;
    try
    {
        num1 = System.Convert.ToInt32(textBox1.Text);
        if (num1 >= 0 && num1 <= 10)
        {
            MessageBox.Show("You have entered : " + textBox1.Text);
        }
        else
        {
            throw new Exception("Number should be between 0 and 10");
        }
    }
    catch (Exception ex)
    {
        MessageBox.Show("Exception occurred " + ex.ToString());
    }
}
```

In Listing 7.8, an integer variable **num1** is declared that stores the value entered in TextBox1. Using the if statement, the value entered in the **num1** variable is checked to see if it is between 0 and 10. If the condition is true, a message box appears, displaying the number entered by the user. If the condition is false, then an exception is thrown and the control is passed to the catch statement.

+   11. *Press* the **F5** key to execute the application. The output is displayed, as shown in Fig.C#-7.26:

![](bbox=[0.399, 0.636, 0.624, 0.81])

Fig.C#-7.26

+   12. *Enter* a value in the **Enter No.(0-10)** textbox. In this case, we have entered the value 12 (Fig.C#-7.27).

+   13. *Click* the **Submit** button, as shown in Fig.C#-7.27: