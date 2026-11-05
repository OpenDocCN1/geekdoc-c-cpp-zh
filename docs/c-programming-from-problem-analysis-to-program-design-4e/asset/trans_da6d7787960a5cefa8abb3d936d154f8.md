
```csharp
// menuDisplayOrder
//
        this.menuDisplayOrder.Name = "menuDisplayOrder";
        this.menuDisplayOrder.Size = new
            System.Drawing.Size(152, 22);
        this.menuDisplayOrder.Text = "Display Order";
        this.menuDisplayOrder.Click += new System.EventHandler
            (this.menuDisplayOrder_Click);

// menuExit
//
        this.menuExit.Name = "menuExit";
        this.menuExit.Size = new System.Drawing.Size(152, 22);
        this.menuExit.Text = "Exit";
        this.menuExit.Click += new System.EventHandler
            (this.menuExit_Click);

// editToolStripMenuItem
//
        this.editToolStripMenuItem.DropDownItems.AddRange
            (new System.Windows.Forms.ToolStripItem[] {
                this.menuEditEntree,
                this.menuEditDrink,
                this.menuEditSpecial});
        this.editToolStripMenuItem.Name =
            "editToolStripMenuItem";
        this.editToolStripMenuItem.Size = new
            System.Drawing.Size(37, 20);
        this.editToolStripMenuItem.Text = "Edit";

// menuEditEntree
//
        this.menuEditEntree.Name = "menuEditEntree";
        this.menuEditEntree.Size = new
            System.Drawing.Size(166, 22);
        this.menuEditEntree.Text = "Entree";
        this.menuEditEntree.Click += new System.EventHandler
            (this.menuEditEntree_Click);

// menuEditDrink
//
        this.menuEditDrink.Name = "menuEditDrink";
        this.menuEditDrink.Size = new
            System.Drawing.Size(166, 22);
        this.menuEditDrink.Text = "Drink";
        this.menuEditDrink.Click += new System.EventHandler
            (this.menuEditDrink_Click);
```
```csharp
//
// menuEditSpecial
//
this.menuEditSpecial.Name = "menuEditSpecial";
this.menuEditSpecial.Size = new
    System.Drawing.Size(166, 22);
this.menuEditSpecial.Text = "Special Requests";
this.menuEditSpecial.Click += new System.EventHandler
    (this.menuEditSpecial_Click);

//
// helpToolStripMenuItem
//
this.helpToolStripMenuItem.DropDownItems.AddRange
    (new System.Windows.Forms.ToolStripItem[] {
        this.menuAbout});
this.helpToolStripMenuItem.Name =
    "helpToolStripMenuItem";
this.helpToolStripMenuItem.Size = new
    System.Drawing.Size(40, 20);
this.helpToolStripMenuItem.Text = "Help";

//
// menuAbout
//
this.menuAbout.Name = "menuAbout";
this.menuAbout.Size = new
    System.Drawing.Size(152, 22);
this.menuAbout.Text = "About";
this.menuAbout.Click += new System.EventHandler
    (this.menuAbout_Click);

//
// OrderGUI
//
this.AutoScaleBaseSize = new
    System.Drawing.Size(6, 15);
this.BackColor = System.Drawing.Color.Goldenrod;
this.ClientSize = new System.Drawing.Size(342, 253);
this.Controls.Add(this.ckBxWater);
this.Controls.Add(this.label2);
this.Controls.Add(this.cmbSpecial);
this.Controls.Add(this.groupBox2);
this.Controls.Add(this.label1);
this.Controls.Add(this.lstBxEntree);
this.Controls.Add(this.menuStrip1);
this.Font = new System.Drawing.Font("Arial", 9.75F,
    System.Drawing.FontStyle.Regular,
    System.Drawing.GraphicsUnit.Point, ((byte)(0)));
this.ForeColor = System.Drawing.Color.Navy;
this.Icon = ((System.Drawing.Icon)(resources.GetObject
    ("$this.Icon")));
this.MainMenuStrip = this.menuStrip1;
this.Name = "OrderGUI";
this.Text = "Student Union   -   Diner by the Valley";
```
```csharp
this.Load += new System.EventHandler(this.OrderGUI_Load);
this.groupBox2.ResumeLayout(false);
this.menuStrip1.ResumeLayout(false);
this.menuStrip1.PerformLayout();
this.ResumeLayout(false);
this.PerformLayout();
}
#endregion  // End of Windows Form Designer generated code

private Order newOrder;
private System.Windows.Forms.Label label1;
private System.Windows.Forms.GroupBox groupBox2;
private System.Windows.Forms.Label label12;
private System.Windows.Forms.ListBox lstBxEntree;
private System.Windows.Forms.ComboBox comboSpecial;
private System.Windows.Forms.CheckBox chkBxWater;
private System.Windows.Forms.RadioButton radCoffee;
private System.Windows.Forms.RadioButton radTea;
private System.Windows.Forms.RadioButton radLemon;
private System.Windows.Forms.RadioButton radSoda;
private System.Windows.Forms.RadioButton radJuice;
private System.Windows.Forms.RadioButton radMilk;
private System.Windows.Forms.MenuStrip menuStrip1;
private ToolStripMenuItem fileToolStripMenuItem;
private ToolStripMenuItem menuPlaceOrder;
private ToolStripMenuItem menuClearOrder;
private ToolStripMenuItem menuDisplayOrder;
private ToolStripMenuItem menuExit;
private ToolStripMenuItem editToolStripMenuItem;
private ToolStripMenuItem menuEditEntree;
private ToolStripMenuItem menuEditDrink;
private ToolStripMenuItem menuEditSpecial;
private ToolStripMenuItem helpToolStripMenuItem;
private ToolStripMenuItem menuAbout;
private System.ComponentModel.IContainer components = null;
}
}  // End of OrderGUI.Designer.cs file
```
```csharp
// OrderGUI.cs        Author: Doyle
// This file contains the event-handler methods.
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Text;
using System.Windows.Forms;

namespace Diner
```
```csharp
{
    public partial class OrderGUI : Form
    {
        public OrderGUI( )
        {
            InitializeComponent( );
        }

        // Instantiates an object of the Order class when
the form is first loaded.
        private void OrderGUI_Load(object sender,
                                   System.EventArgs e)
        {
            newOrder = new Order( );
            for(int i = 0; i < newOrder.menuEntree.Length; i++)
            {
                this.lstBxEntree.Items.Add
                    (newOrder.menuEntree[i]);
            }
        }

        // Event handler that gets the entree from the
        // ListBox and sets the entree price.
        private void lstBxEntree_SelectedIndexChanged
            (object sender, System.EventArgs e)
        {
            newOrder.Entree = this.lstBxEntree.Text;
        }

        // Event handler that gets the special request -
        // if one is selected from the predefined list.
        private void cmbSpecial_SelectedIndexChanged
            (object sender, System.EventArgs e)
        {
            newOrder.SpecialRequest =
                this.cmbSpecial.Text;
        }

        // Menu item that displays the order
        private void menuDisplayOrder_Click(object sender,
                                            System.EventArgs e)
        {
            MessageBox.Show
                (newOrder.Entree + "\n"
                    + newOrder.SpecialRequest
                    + "\n"
                    + newOrder.DrinkSelection
                    + "\n" +
                    newOrder.GetWaterSelection( ),
                    "Current Order");
        }
    }
}
```
```csharp
// Event handler that gets the radio button
// selected and sets the drink selection.
private void Drink_CheckedChanged(object sender,
    System.EventArgs e)
{
    if (this.radTea.Checked)
        newOrder.DrinkSelection = radTea.Text;
    else
        if (this.radCoffee.Checked)
            newOrder.DrinkSelection = radCoffee.Text;
        else
            if (this.radSoda.Checked)
                newOrder.DrinkSelection = radSoda.Text;
            else
                if (this.radLemon.Checked)
                    newOrder.DrinkSelection = radLemon.Text;
                else
                    if (this.radJuice.Checked)
                        newOrder.DrinkSelection =
                            radJuice.Text;
                    else
                        if (this.radMilk.Checked)
                            newOrder.DrinkSelection =
                                radMilk.Text;
}

// Event handler that gets raised when the check box
// for Water gets clicked.
private void ckbxWater_CheckedChanged
    (object sender, System.EventArgs e)
{
    if (this.ckbxWater.Checked)
        newOrder.WaterSelection = true;
    else
        newOrder.WaterSelection = false;
}

// Event handler that gets raised when the
// user types values into the text area of
// the combo box.
private void cmboSpecial_KeyPress (object sender,
    System.Windows.Forms.KeyPressEventArgs e)
{
    newOrder.SpecialRequest =
        this.cmboSpecial.Text;
}
```
