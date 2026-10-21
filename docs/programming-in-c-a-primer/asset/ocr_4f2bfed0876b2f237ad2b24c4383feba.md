In the above code, we have set the Height and Width properties of the form object to 125 and 250 respectively. Thus, the generated output form will change its size accordingly.

# 20.3.3 Customizing the Colors

The BackColor property of the Form class enables us to modify the background color of a form. The choice of the colors can be made from the Color structure contained in the System.Drawing namespace.

The following code makes use of the BackColor property to change the background color of the F1 form object.

```
```csharp
//Program - SampleForm.cs
using System.Windows.Forms;
using System.Drawing;
public class SampleForm : Form
{
	public static void Main()
	{
		SampleForm F1 = new SampleForm();
		F1.BackColor = Color.Green;
		F1.Text = "My Form";
		Application.Run(F1);
	}
}
```
```

Figure 20.4 shows the output of the above code:

![](bbox=[0.25, 0.65, 0.75, 0.85])

Fig. 20.4 Customizing the background color of a form