# A member list that's displayed in the Code Editor window

```
csharp
private void btnCalculate_Click(object sender, EventArgs e)
{
    decimal subtotal = 
        Convert.ToDecimal(txtSubtotal.Text);
    // AppendText
    // ResetText
    // Text
    // TextAlignment
    // TextAlignChanged
    // TextChanged
    // TextLength
    // Gets or sets the current text in the System.Windows.Forms.TextBox.
```

# The syntax for referring to a member of a class or object

ClassName.MemberName
objectName.MemberName

# Statements that refer to properties

| txtTotal.Text = "10"; | Assigns a string holding the 10 to the Text property of the text box named txtTotal. |
| txtTotal.ReadOnly = true; | Assigns the true value to the ReadOnly property of the text box named txtTotal so the user can't change its contents. |

# Statements that refer to methods

| txtMonthlyInvestment.Focus(); | Uses the Focus method to move the focus to the text box named txtMonthlyInvestment |
| this.Close(); | Uses the Close method to close the form that contains the statement. In this example, this is a keyword that is used to refer to the current instance of the class. |

# Code that refers to an event

| btnExit.Click | Refers to the Click event of a button named btnExit. |

# How to enter member names when working in the Code Editor

+   - To display a list of available members for a class or object, type the object name followed by a period (called a dot operator, or just dot). You can type one or more letters of the member name, and the Code Editor will select the first entry in the list that matches those letters. Or, you can scroll down the list to select the member you want. Once it's selected, press the Tab or Enter key to insert the member into your code.
- If a member list isn't displayed, use the Tools>Options command to display the Options dialog box. Then, expand the Text Editor, select the C# category, and check the Auto List Members and Parameters information boxes.

Figure 3-2 How to refer to properties, methods, and events