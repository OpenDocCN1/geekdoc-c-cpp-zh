# Example 10-20

```
```csharp
// GardeningForm.cs    Author: Doyle
// Menu, ListBox, ComboBox, Label, and TextBox
// Objects are included in the design. KeyPress( ),
// Click( ), and SelectedIndexChanged( )
// are programmed. Font and Color dialog boxes
// are added.
using System;
using System.Drawing;
using System.Collections.Generic;
using System.ComponentModel;
using System.Windows.Forms;
using System.Data;
using System.Text;
namespace GardeningForm
{
    public partial class GardeningForm : System.Windows.Forms.Form
    {
        public GardeningForm( )
        {
            InitializeComponent( );
        }

        private void cmbOfFlowers_SelectedIndexChanged
                (object sender, System.EventArgs e)
        {
            this.txtBoxResultFlowers.Text =
                    this.cmbOfFlowers.Text;
        }

        private void cmbOfFlowers_KeyPress
                (object sender,
                 System.Windows.Forms.KeyPressEventArgs e)
        {
            this.txtBoxResultFlowers.Text =
                    cmbOfFlowers.Text;
        }

        private void lstBoxTrees_SelectedIndexChanged
                (object sender, System.EventArgs e)
        {
            this.txtBoxResultTrees.Text = " ";
            foreach (int i in lstBoxTrees.SelectedIndices)
            {
                this.txtBoxResultTrees.Text +=
                        this.lstBoxTrees.Items[i] + " ";
            }
```
```