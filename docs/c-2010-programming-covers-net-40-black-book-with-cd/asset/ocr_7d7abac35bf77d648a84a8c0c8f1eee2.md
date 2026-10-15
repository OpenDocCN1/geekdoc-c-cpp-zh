```
con.Open();
string command = "select OrderID, ProductID, Quantity from [Order Details] where Quantity > 61 and Quantity < 90";
SqlCommand cmd = new SqlCommand(command, con);
SqlDataAdapter adp = new SqlDataAdapter(cmd);
DataSet ds = new DataSet();
adp.Fill(ds, "Order Details");
dataGridView1.DataSource = ds.Tables[0];
}
else
{
SqlConnection con = new SqlConnection("data Source=.;Initial Catalog=Northwind;Integrated Security=True");
con.Open();
string command = "select OrderID, ProductID, Quantity from [Order Details]";
SqlCommand cmd = new SqlCommand(command, con);
SqlDataAdapter adp = new SqlDataAdapter(cmd);
DataSet ds = new DataSet();
adp.Fill(ds,"Order Details");
dataGridView1.DataSource = ds.Tables[0];
}
}
```

After adding the code given in Listing 25.4, run the CheckBoxControl application by pressing the F5 key. The Form1 form appears, displaying the CheckBox and the DataGridView controls. To sort the data of the OrderDetails table, select any of the three CheckBox controls. In our case, we have selected the checkbox beside 30-60 option. The final output of the CheckBoxControl application, is shown in Figure 25.11:

![](bbox=[0.29, 0.49, 0.62, 0.68])

Figure 25.11: Displaying the Data on the Basis of the CheckBox Controls

# Combo Boxes

Let’s now learn to bind data to a ComboBox control. To do this, create a Windows Forms Application, named ComboBoxControl (also available on the CD) and add a ComboBox control to Form1. After adding the control, add the code in Listing 25.5 to the Form1.cs file, which is the code-behind file of your application:

Listing 25.5: Showing the Code of the ComboBoxControl Application

```
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
```