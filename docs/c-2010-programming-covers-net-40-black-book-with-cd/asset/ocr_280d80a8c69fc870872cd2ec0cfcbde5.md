Perform the following steps to create the `GenericDictionarySample` application:

+   1. Set the Text property of Form1 to Generic Dictionary Sample.
+   2. Drag and drop a ListView, a GroupBox, and three Button controls to the form.
+   3. Set the Text property of the GroupBox control to Noteworthy Operations and the Text property of button1 to Create and add 10 items, button2 to ContainsKey, and button3 to ContainsValue.
+   4. Add columns to the ListView control by clicking the ellipse button (...) of the Columns property of the ListView control in the Properties window. The ColumnHeader Collection Editor dialog box appears.
+   5. Click the Add button to add a column to the ListView control in the ColumnHeader Collection Editor dialog box. Set the Name property of this column to Key and the Text property to Keys. Similarly, add another column to the ListView control with the name as Value and text set to Values, and then click the OK button.
+   6. Add the code given in Listing 32.10 to the Form1.cs file of the GenericDictionarySample application:

```
Listing 32.10: Showing the Code of the GenericDictionarySample Application

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace GenericDictionarySample
{
    public partial class Form1 : Form
    {
        Dictionary<int, string> dictStr = new Dictionary<int, string>();
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            button2.Enabled = false;
            button3.Enabled = false;
        }
        private void button1_Click(object sender, EventArgs e)
        {
            dictStr.Add(100, "White");
            dictStr.Add(101, "Black");
            dictStr.Add(102, "Blue");
            dictStr.Add(103, "Yellow");
            dictStr.Add(104, "Green");
            dictStr.Add(105, "Red");
            dictStr.Add(106, "Orange");
            dictStr.Add(107, "Purple");
            dictStr.Add(108, "Magenta");
            dictStr.Add(109, "Brown");
            LoadDictionary();
            button2.Enabled = true;
            button3.Enabled = true;
        }
        private void LoadDictionary()
        {
            listview1.Items.Clear();
            foreach (object obj in dictStr.Keys)
```