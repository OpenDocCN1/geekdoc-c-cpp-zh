```
```csharp
// Calculate take-home pay after deductions.
public void DetermineNet()
{
    net = gross - socialSecurity - federalTax - agencyFee;
}
```
```

![](bbox=[0.189, 0.2, 0.251, 0.249])

The program listing for the file containing the source code for the class that creates the graphical user interface appears next. For brevity, the TempAgencyForm is shown as a single source code file. The program statements for the form would be divided into three separate source code files.

```
```csharp
// TempAgencyForm.cs          Author: Doyle
// Builds the Graphical User Interface
// Includes button, label, textbox, and form objects
using System;
using System.Drawing;
using System.Collections;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
namespace PayRollApp
{
    public class TempAgencyForm : System.Windows.Forms.Form
    {
        private System.Windows.Forms.Label label1;
        private System.Windows.Forms.Label label4;
        private System.Windows.Forms.Label lblNet;
        private System.Windows.Forms.Label lblFed;
        private System.Windows.Forms.Label lblGross;
        private System.Windows.Forms.Label lblSoc;
        private System.Windows.Forms.Label lblAgency;
        private System.Windows.Forms.TextBox txtGross;
        private System.Windows.Forms.TextBox txtFed;
        private System.Windows.Forms.TextBox txtSoc;
        private System.Windows.Forms.TextBox txtAgency;
        private System.Windows.Forms.Button btnCalculate;
        private System.Windows.Forms.TextBox txtName;
        private System.Windows.Forms.TextBox txtHours;
        private System.Windows.Forms.TextBox txtDep;
        private System.Windows.Forms.Label lblHours;
        private System.Windows.Forms.Label lblDep;
        private System.Windows.Forms.Button btnReset;

        // Required designer variable
        private System.ComponentModel.Container components = null;
```
```