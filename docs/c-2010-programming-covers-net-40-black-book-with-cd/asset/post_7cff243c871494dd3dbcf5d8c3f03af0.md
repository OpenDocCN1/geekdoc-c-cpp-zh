
```
private void quantityToolStripMenuItem_Click(object sender, EventArgs e)
{
    listBox1.DataSource = northwindDataSet;
    listBox1.DisplayMember = "Order Details.Quantity";
}
private void discountToolStripMenuItem_Click(object sender, EventArgs e)
{
    listBox1.DataSource = northwindDataSet;
    listBox1.DisplayMember = "Order Details.Discount";
}
private void exitToolStripMenuItem_Click(object sender, EventArgs e)
{
    Close();
}
private void button1_Click(object sender, EventArgs e)
{
    this.BindingContext[northwindDataSet, "Order Details"].Position =
    (this.BindingContext[northwindDataSet, "Order Details"].Position + 1);
    toolStripStatusLabel1.Text = "You are currently at Record " +
        Convert.ToString(this.BindingContext[northwindDataSet, "Order Details"].Position + 1) + " of " +
        Convert.ToString(this.BindingContext[northwindDataSet, "Order Details"].Count);
}
```

The MenuandStatusStrip application is connected to the Order Details table of the Northwind database. Now, click a submenu from the File menu. Depending upon your selection of the submenu, the data is displayed in the ListBox control, as shown in Figure 25.15:

![](img/e073a4882197be4ab61103cbe0bcb394_1231_0.png)

The position of the record in the original dataset is displayed in the StatusStrip control (Figure 25.15).

> **NOTE**
> 
> The data in the DataGridView control is retrieved by using the Data Configuration wizard.

## Using the BindingContext Class

The BindingContext class provides information about binding various data elements in a Windows application. The inheritance hierarchy of the BindingContext class is given as follows:

```
System.Object
System.Windows.Forms.BindingContext
```

Each object that inherits from the Control class can have a single BindingContext object, which helps you to access the data bindings in a form.

Table 25.2 lists the noteworthy public properties of the BindingContext class:

Table 25.2: Noteworthy Public Properties of the BindingContext Class

| Property | Description |
|---|---|
| Item | Retrieves an object of the BindingManagerBase class that is associated with data source and data member |
| IsReadOnly | Retrieves a value indicating whether the collection is read-only |

Table 25.3 lists the noteworthy methods of the BindingContext class:

Table 25.3: Noteworthy Public Methods of BindingContext Class

| Method | Description |
|---|---|
| Contains() | Specifies whether or not the BindingContext class contains a particular item |
| UpdateBinding() | Associates a binding with a new BindingContext object |

The BindingContext object's Position property is used to move through a dataset. Let's create a Windows Forms application, named NavigatingRecords (also available on the CD), to display the current location of a record in a dataset. Add the code provided in Listing 25.9 to the Form1.cs file, which is the code-behind file of your application:

### Listing 25.9: Showing the Code of the NavigatingRecords Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
namespace NavigatingRecords
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void Form1_Load(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the 'northwindDataSet.Employees' table. You can move or remove it, as needed.
            this.employeesTableAdapter.Fill(this.northwindDataSet.Employees);
            listBox1.DataSource = northwindDataSet;
            listBox1.DisplayMember = "Employees.FirstName";
            listBox1.ValueMember = "Employees.EmployeeID";
```

```
comboBox1.DataSource = northwindDataSet;
comboBox1.DisplayMember = "Employees.City";
comboBox1.ValueMember = "Employees.EmployeeID";
textBox1.DataBindings.Add(new Binding("Text", northwindDataSet, "Employees.EmployeeID"));
textBox2.DataBindings.Add(new Binding("Text", northwindDataSet, "Employees.HomePhone"));
toolStripStatusLabel1.Text = "You are currently at Record " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Position
+ 1)
+ " of " + Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Count);
}
private void button1_Click(object sender, EventArgs e)
{
this.BindingContext[northwindDataSet, "Employees"].Position = 0;
toolStripStatusLabel1.Text = "You are currently at Record " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Position + 1) + " of " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Count);
}
private void button2_Click(object sender, EventArgs e)
{
this.BindingContext[northwindDataSet, "Employees"].Position =
(this.BindingContext[northwindDataSet, "Employees"].Position - 1);
toolStripStatusLabel1.Text = "You are currently at Record " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Position + 1) + " of " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Count);
}
private void button3_Click(object sender, EventArgs e)
{
this.BindingContext[northwindDataSet, "Employees"].Position =
(this.BindingContext[northwindDataSet, "Employees"].Position + 1);
toolStripStatusLabel1.Text = "You are currently at Record " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Position + 1) + " of " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Count);
}
private void button4_Click(object sender, EventArgs e)
{
this.BindingContext[northwindDataSet, "Employees"].Position =
(this.BindingContext[northwindDataSet, "Employees"].Count - 1);
toolStripStatusLabel1.Text = "You are currently at Record " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Position + 1) + " of " +
Convert.ToString(this.BindingContext[northwindDataSet, "Employees"].Count);
}
}
```

Now, run the NavigatingRecords application by pressing the F5 key. The output of the NavigatingRecords application is shown in Figure 25.16:

![](img/e073a4882197be4ab61103cbe0bcb394_1234_0.png)

## Figure 25.16: Navigating Records

As shown in Figure 25.16, you can navigate through the records in the dataset by using the four button controls located in the Navigational Panel. The following is the list of functions performed by these buttons:

- button1 — Moving to the first record
- button2 — Moving to the previous record
- button3 — Moving to the next or current record
- button4 — Moving to the last record

## Moving to the First Record

To move to the first record in the NavigatingRecords application, you need to set the Position property of the dataset to 0. The code given in the following code snippet needs to be inserted in the Click event of button1 to make it show the first record in the dataset:

```
private void button1_Click(object sender, EventArgs e)
{
    this.BindingContext[northwindDataSet, "Employees"].Position = 0;
    toolStripStatusLabel1.Text = "You are currently at Record " +
    Convert.ToString(this.BindingContext[northwindDataSet,
    "Employees"].Position + 1) + " of " +
    Convert.ToString(this.BindingContext[northwindDataSet,
    "Employees"].Count);
}
```

You can move to the first record in the ListBox control by clicking the << button from the Navigational Panel (Figure 25.16).

## Moving to the Previous Record

To move to the previous record in the NavigatingRecords application, you need to decrement the value of the Position property. The code given in the following code snippet needs to be inserted in the Click event of button2 to make it show the previous record in the dataset:

```
private void button2_Click(object sender, EventArgs e)
{
    this.BindingContext[northwindDataSet, "Employees"].Position =
    (this.BindingContext[northwindDataSet, "Employees"].Position - 1);
    toolStripStatusLabel1.Text = "You are currently at Record " +
    Convert.ToString(this.BindingContext[northwindDataSet,
```
