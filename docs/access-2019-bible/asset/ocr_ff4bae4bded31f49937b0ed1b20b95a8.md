# Creating an interactive filter dialog box

> **CAUTION**
> You can only use like "*" with text fields. For numeric fields, you can set the criteria to [My Prompt] OR [My Prompt] IS NULL. Just be certain that both occurrences of My Prompt are typed identically. (Copy and paste is a good idea.) You can also use this technique with text fields if you want to return all the records including those with null values.

The problem with parameter queries is that they’re only suitable for simple parameters. The users have to know exactly what to type into the parameter dialog box, and if they enter the parameter incorrectly, they won’t see the results they expect. Also, using parameter queries for entering complex criteria is fairly difficult.

A better technique is to create a simple form, place controls on the form, and reference the controls from a query as parameters. In other words, the query uses the form’s controls to get its parameter values. This is a huge advantage to the users because the controls can help the user select the criteria by presenting lists or drop-down menus of the acceptable parameter values. Plus, code can be added to each control’s AfterUpdate event to validate the user’s input to ensure that the query will actually run. The content of controls like combo boxes or list boxes can be dynamic and contain actual values from the underlying tables. This means that the criteria controls might contain only the names of customers who’ve placed orders, or product categories actually in the database at the moment.

Figure 29.10 shows frmFilterProducts in Design view. cboCategory is filled with the data from qryCategories, which sorts the records in tblCategories in alphabetical order.

# FIGURE 29.10

Creating a dialog box for selecting records.

![](bbox=[0.167, 0.619, 0.671, 0.902])