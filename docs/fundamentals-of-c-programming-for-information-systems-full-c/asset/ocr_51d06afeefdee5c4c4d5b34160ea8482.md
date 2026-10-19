Step 5-2: Open the code window and add the missing class-level code from Figure 12-52 to create the data access objects for Department.

Step 5-3: Add the missing code from Figure 12-54 to the Load event handler of the form to display DeptNo’s in the ComboBoxes.

Step 5-4: Run the form and test the code. The ComboBoxes should display the DeptNo’s.

# Filtering Rows Using the Binding Source

Filtering involves using the Filter property of the binding source to select rows from the data table for display in controls on the form. Section 12.7 discussed filtering using data objects created at design time using the wizard. The process is the same for untyped data tables. To refresh your memory, the syntax of the statement to filter rows from the data table is

```
bindingSource.Filter = "criterion";
```

where bindingSource is the name of the binding source object, and criterion is any Boolean expression. Examples of the statement for string and numeric fields can be found in Section 12.7.

In the Employee_Search form, the criterion is that the employee’s DeptNo should be equal to the value selected in the cboFilterByDept ComboBox. Figure 12-55 shows the code that specifies the criterion.

Because we want the selected rows to be displayed whenever the user selects a DeptNo from the ComboBox, the code is placed in the SelectionChangeCommitted event handler of the ComboBox. The SelectionChangeCommitted event is fired when the user selects an item from the ComboBox.

As discussed in Section 12.7, the SelectedIndexChanged event is less suitable because it is fired under other conditions, too.

# Figure 12-55: Filtering using the binding source

```
61  private void cboFilterByDept_SelectionChangeCommitted(object sender, EventArgs e)
62  {
63      bsEmployee.Filter = "DeptNo = " + cboFilterByDept.SelectedValue.ToString();
64      if (bsEmployee.Count > 0)
65      {
66          lblRecordNo.Text = (bsEmployee.Position + 1) + " of " + bsEmployee.Count;
67          DisplayCurrentRow();
68      }
}
```

Step 5-5: Generate the SelectionChangeCommitted event handler for cboFilterByDept ComboBox. (Select cboFilterByDept. In the properties window, click on the events button [lightning bolt]. Double click the SelectionChangeCommitted event).

Add the code from Figure 12-55 to the event handler to filter records. Run the form and test the code by selecting the value 3 from the cboFilterByDept. You should be able to see only two employee records.