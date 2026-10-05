# The generated code for a parameterized query

```
private void fillByCustomerIDIDToolStripButton_Click(
    object sender, EventArgs args)
{
    try
{
        this.customersTableAdapter.FillByCustomerID(
            this.mmaBooksDataSet.Customers,
            ((int) System.Convert.ChangeType(customerIDToolStripTextBox.Text, typeof(int))));
    }
    } catch (System.Exception ex)
    {
        System.Windows.Forms.MessageBox.Show(ex.Message);
    }
}
```

# The same code after it has been cleaned up and enhanced

```
private void fillByCustomerIDIDToolStripButton_Click(
    object sender, EventArgs args)
{
    try
{
        int customerID = Convert.ToInt32(customerIDToolStripTextBox.Text);

        this.customersTableAdapter.FillByCustomerID(
            this.mmaBooksDataSet.Customers,
            customerID);
    }
    } catch (Exception ex)
    {
        MessageBox.Show(ex.Message, ex.GetType().ToString());
    }
}
```

# The syntax of the method for filling a table using a parameterized query

tableAdapter.QueryName(dataSet.TableName, param1 ,param2...)

# Description

+   - When you finish specifying a query in the Search Criteria Builder dialog box, Visual Studio automatically generates the code that uses the appropriate method to fill the table in the dataset when the user clicks the button in the toolbar.
- If necessary, you can modify the generated code to make it easier to read or to change the way it works.

![](bbox=[0.066, 0.943, 0.638, 0.958])