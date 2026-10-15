![](bbox=[0.24, 0.07, 0.78, 0.36])

# Figure 8.18: Modifying the Properties of Controls

+   9. Add a TextBox, textBox1, to Form2.

+   10. Enter the Displaying Second Form text in the Text property of the textBox1 control in Form2.

+   11. Add the following code snippet in the Click event of the button1 control of Form1:

```
private void button1_Click(object sender, EventArgs e)
{
    Form2 secondForm = new Form2();
    secondForm.Message = textBox1.Text.ToString();
    secondForm.Show();
}
```

In the preceding code snippet, we have created an object of Form2. In addition, we have used the Message property of Form2 to retrieve the text from the textBox1 control of Form1.

+   12. Replace the code given in the Form2.cs file with the code given in Listing 8.1:

# Listing 8.1: Modifying the Code of the Form2.cs File

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace MultiForm {
public partial class Form2 : Form {
    private string strMessage;
    public string Message
    {
        get {
            return strMessage;
        }
        set {
            strMessage = value;
        }
    }
    public Form2()
    {
        InitializeComponent();
```