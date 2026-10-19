Step 2-7: Set the DataBindings property of EmpId ComboBox to None, as shown in Figure 12-30.

# Figure 12-30: Setting the DataBindings property of EmpId ComboBox to None

![](bbox=[0.034, 0.14, 0.548, 0.356])

Step 2-8: Run the form. Select an id from the EmpId ComboBox and verify that the record for the selected id is displayed.

How does it find the record when there is no code to do it? The secret is that the ComboBox is getting the EmpIds from the Employee data table that also is bound to other controls on the form. So, when you select an EmpId from the ComboBox, you are changing the current record in the Employee data table, which in turn changes the data in all bound controls. This won’t happen if you bind the ComboBox to one data table and the other controls to a different data table.

It’s time to practice! Do Exercise 12-1.

# Review Question

12.8 The data from a table named Customer is displayed on a form in Details View. The controls on the form were created by dragging and dropping the data table on the form after changing CustomerId field to a ComboBox. The purpose of the ComboBox is to let the user select a CustomerId from a list of all CustomerIds and display the record for the selected id. What properties of the ComboBox need to be changed from the default setting? What should be the setting for those properties?