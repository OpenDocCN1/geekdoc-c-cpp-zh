
```csharp
// Clean up any resources being used.
protected override void Dispose(bool disposing)
{
    if (disposing && (components != null))
    {
        components.Dispose();
    }
    base.Dispose(disposing);
}

#region Windows Form Designer generated code

// Required method for Designer support - do not modify
// the contents of this method with the code editor.
private void InitializeComponent()
{
    this.label1 = new System.Windows.Forms.Label();
    this.label2 = new System.Windows.Forms.Label();
    this.label3 = new System.Windows.Forms.Label();
    this.label4 = new System.Windows.Forms.Label();
    this.label5 = new System.Windows.Forms.Label();
    this.txtPurchase = new System.Windows.Forms.TextBox();
    this.txtTotalDue = new System.Windows.Forms.TextBox();
    this.btnCompute = new System.Windows.Forms.Button();
    this.SuspendLayout();
    //
    // label1
    //
    this.label1.AutoSize = true;
    this.label1.Location = new System.Drawing.Point(37, 51);
    this.label1.Name = "label1";
    this.label1.Size = new System.Drawing.Size(120, 20);
    this.label1.TabIndex = 0;
    this.label1.Text = "Total Amount:";
    //
    // label2
    //
    this.label2.AutoSize = true;
    this.label2.Location = new System.Drawing.Point(37, 98);
    this.label2.Name = "label2";
    this.label2.Size = new System.Drawing.Size(133, 20);
    this.label2.TabIndex = 1;
    this.label2.Text = "Tax Percentage:";
    //
    // label3
    //
    this.label3.AutoSize = true;
    this.label3.Location = new System.Drawing.Point(37, 145);
    this.label3.Name = "label3";
    this.label3.Size = new System.Drawing.Size(90, 20);
    this.label3.TabIndex = 2;
    this.label3.Text = "Total Due:";
    //
    // label4
    //
    this.label4.AutoSize = true;
    this.label4.Font = new System.Drawing.Font
        ("Bookman Old Style", 12F, System.Drawing.FontStyle.Bold,
        System.Drawing.GraphicsUnit.Point, ((byte)(0)));
    this.label4.Location = new System.Drawing.Point(109, 13);
    this.label4.Name = "label4";
    this.label4.Size = new System.Drawing.Size(128, 19);
    this.label4.TabIndex = 3;
    this.label4.Text = "Tax Calculator";
    this.label4.Click += new System.EventHandler
        (this.btnCompute_Click);
    //
    // label5
    //
    this.label5.AutoSize = true;
    this.label5.BackColor = System.Drawing.Color.FromArgb(((int)
        (((byte)(50)))), (((int)(((byte)(50)))),
        ((int)(((byte)(192))))));
    this.label5.ForeColor = System.Drawing.Color.FromArgb(((int)
        (((byte)(128)))), (((int)(((byte)(128)))),
        ((int)(((byte)(255))))));
    this.label5.Location = new System.Drawing.Point(185, 98);
    this.label5.Name = "label5";
    this.label5.Size = new System.Drawing.Size(48, 20);
    this.label5.TabIndex = 4;
    this.label5.Text = "7.5%";
    //
    // txtPurchase
    //
    this.txtPurchase.Location = new
        System.Drawing.Point(180, 50);
    this.txtPurchase.Name = "txtPurchase";
    this.txtPurchase.Size = new System.Drawing.Size(100, 26);
    this.txtPurchase.TabIndex = 5;
    this.txtPurchase.TextAlign =
        System.Windows.Forms.HorizontalAlignment.Right;
    //
    // txtTotalDue
    //
    this.txtTotalDue.Enabled = false;
    this.txtTotalDue.Location = new
        System.Drawing.Point(180, 144);
    this.txtTotalDue.Name = "txtTotalDue";
    this.txtTotalDue.Size = new System.Drawing.Size(100, 26);
    this.txtTotalDue.TabIndex = 6;
    this.txtTotalDue.TextAlign =
        System.Windows.Forms.HorizontalAlignment.Right;
    //
    // btnCompute
    //
    this.btnCompute.BackColor = System.Drawing.Color.Navy;
    this.btnCompute.Font = new
        System.Drawing.Font("Bookman Old Style", 14F,
        System.Drawing.FontStyle.Bold,
        System.Drawing.GraphicsUnit.Point, ((byte)(0)));
    this.btnCompute.ForeColor =
        System.Drawing.Color.FromArgb(((int)(((byte)(255)))),
        ((int)(((byte)(255)))), ((int)(((byte)(128)))));
    this.btnCompute.Location = new
        System.Drawing.Point(114, 196);
    this.btnCompute.Name = "btnCompute";
    this.btnCompute.Size = new
        System.Drawing.Size(119, 34);
    this.btnCompute.TabIndex = 2;
    this.btnCompute.Text = "Compute";
    this.btnCompute.UseVisualStyleBackColor = false;
    this.btnCompute.Click += new
        System.EventHandler(this.btnCompute_Click);
    //
    // Form1
    //
    this.AcceptButton = this.btnCompute;
    this.AutoScaleDimensions = new
        System.Drawing.SizeF(10F, 20F);
    this.AutoScaleMode =
        System.Windows.Forms.AutoScaleMode.Font;
    this.BackColor = System.Drawing.Color.FromArgb(((int)
        (((byte)(192)))), ((int)(((byte)(192)))),
        ((int)(((byte)(255)))));
    this.ClientSize = new System.Drawing.Size(310, 242);
    this.Controls.Add(this.btnCompute);
    this.Controls.Add(this.txtTotalDue);
    this.Controls.Add(this.txtPurchase);
    this.Controls.Add(this.label5);
    this.Controls.Add(this.label4);
    this.Controls.Add(this.label3);
    this.Controls.Add(this.label2);
    this.Controls.Add(this.label1);
    this.Font = new System.Drawing.Font("Bookman Old Style",
        12F, System.Drawing.FontStyle.Regular,
        System.Drawing.GraphicsUnit.Point, ((byte)(0)));
    this.Margin = new System.Windows.Forms.Padding(4);
    this.Name = "Form1";
    this.Text = "Windows Tax App";
    this.ResumeLayout(false);
    this.PerformLayout();

}
#endregion

private System.Windows.Forms.Label label1;
private System.Windows.Forms.Label label2;
private System.Windows.Forms.Label label3;
private System.Windows.Forms.Label label4;
private System.Windows.Forms.Label label5;
private System.Windows.Forms.TextBox txtPurchase;
private System.Windows.Forms.TextBox txtTotalDue;
private System.Windows.Forms.Button btnCompute;
}
} // End of Form1.Designer.cs file
```

```csharp
// Form1.cs
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace TaxApp
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void btnCompute_Click(object sender, EventArgs e)
        {
            string inValue;
            double purchaseAmt,
                   percent,
                   ans;

            while (double.TryParse(txtPurchase.Text, out purchaseAmt) == false)
            {
                MessageBox.Show("Value entered must be numeric");
                txtPurchase.Text = "0.0";
                txtPurchase.Focus();
            }
            inValue = label5.Text;
            inValue = inValue.Remove(inValue.Length - 1, 1);
            percent = double.Parse(inValue) / 100;
            ans = (purchaseAmt * percent) + purchaseAmt;
            txtTotalDue.Text = string.Format("{0:C}", ans).ToString();
        }
    }
}
```

## PROGRAMMING EXAMPLE: TempAgency Application

This example demonstrates the design and implementation of a graphical user interface for a Windows application. Two classes are constructed to separate the business logic from the presentation details. The first class defines a template for a typical payroll employee object. It includes the behaviors for determining withholding deductions and calculating the net take-home pay; thus, the business logic is described in this Employee class. The other class instantiates an object of the Employee class and instantiates a Windows Form object to represent the graphical user interface. Using the .NET predefined Control classes, labels, text boxes, and button objects are added to the Form object. The problem specification for the TempAgency application is shown in Figure 9-16.

![](img/36e48639a06772bcb0fa1ea2525b33a3_581_0.png)

**FIGURE 9-16** Problem specification for TempAgency

### ANALYZE THE PROBLEM

You should review the problem specification in Figure 9-16 and make sure you understand the problem definition. Several values will be entered into the program to represent the name, number of hours worked, and number of dependents for an employee. The business logic is separated from the user interface by using two separate classes. This enables other applications to use the Employee class. Actual checks for the XYZ JobSource temp agency may need to be printed, payroll records saved, and other reports generated. By separating the logic from the design of the GUI presentation, the Employee class can be reused for many other applications.

### DATA

Table 9-9 lists the data field members needed for the Employee class. In addition to these entered values, instance variables to store deductions and pay amounts are needed.

**TABLE 9-9** Instance field members for the Employee class

| Data description | Type | Identifier |
|---|---|---|
| Employee last name | `string` | `employeeLastName` |
| Employee first name | `string` | `employeeFirstName` |
| Number of dependents | `int` | `noOfDependents` |
| Number of hours worked | `double` | `noOfHours` |

### CONSTANTS

For this example, several values such as hourly rate, Social Security, and federal withholding tax rates are the same for all employees. The user does not have to enter these values at run time; instead, constants can be defined for the values in the Employee class in the methods that use their values. Any objects instantiated of that class can then have access to the amounts, as shown in Table 9-10.

**TABLE 9-10** Constant field members for the Employee class

| Data description | Type | Identifier | Value |
|---|---|---|---|
| Hourly rate | `double` | `RATE` | 150.00 |
| Federal tax deduction percentage | `double` | `FEDERAL_TAX` | 0.25 |
| Social Security deduction percentage | `double` | `SOCIAL_SECURITY_RATE` | 0.0785 |
| Dependent allowance percentage | `double` | `DEPENDENT_ALLOWANCE` | 0.0575 |
| Agency fee for the contract | `double` | `AGENCY_CHARGE` | 0.13 |
