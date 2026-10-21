In the above code, we have disabled the display of the control box, maximize button and minimize button. Also, no text string has been specified for the form caption, thus making the entire caption disappear from the form, as shown in Fig. 20.3.

![](bbox=[0.31, 0.15, 0.7, 0.42])

# 20.3.2 Customizing the Size

The Form class supports a number of properties to enable the programmer to specify the size related settings of a form. Some of these properties are

+   - DefaultSize: Sets the default size of a form
+   - Height: Sets the height of a form
+   - Width: Sets the width of a form
+   - MaximumSize: Sets the maximum size of a form
+   - MinimumSize: Sets the minimum size of a form
+   - StartPosition: Helps specify the initial position of the form

Now, let us modify the SampleForm.cs program to set the size-related properties

# Program 20.3 MODIFYING THE SAMPLE FORM.CS PROGRAM TO SET SIZE-RELATED PROPERTIES

```
//Program - SampleForm.cs
using System.Windows.Forms;
public class SampleForm : Form
{
    public static void Main()
    {
        SampleForm F1 = new SampleForm();
        F1.Height = 125;
        F1.Width = 250;
        F1.Text = "My Form";
        Application.Run(F1);
    }
}
```