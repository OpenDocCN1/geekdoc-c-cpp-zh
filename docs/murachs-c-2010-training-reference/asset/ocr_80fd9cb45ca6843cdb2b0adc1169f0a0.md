# Chapter 10 More skills for working with Windows forms and controls

# The generated code for a new form named frmPayment
For the frmPayment.cs file

```
namespace Payment
{
    public partial class frmPayment : Form
    {
        public frmPayment()
        {
            InitializeComponent();
        }
    }
}
```

# For the frmPayment.Designer.cs file
namespace Payment

```
{
    partial class frmPayment
    {
        #region Windows Form Designer generated code
    }
}
```

# The code that's generated for the Load event handler of the form
The method declaration in the frmPayment.cs file

```
private void frmPayment_Load(object sender, System.EventArgs e)
{
    // code that handles the event goes here
}
```

# The wiring in the frmPayment.Designer.cs file

```
this.Load += new System.EventHandler(this.frmPayment_Load);
```

# Description

+   - The name you specify for the form in the Add New Item dialog box is used by both files for the form class and it appears several times in the generated code.
- Visual Studio uses the name of the form when you create an event handler for one of the form's events such as the Load event.

Figure 10-8 The code that's generated for a new form