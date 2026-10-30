# Feedback 3.4

+   1. Where do you place the binding source and TableAdapter for a multi-tier project?
+   2. What return type is necessary for a function in the class that fills a DataSet from a TableAdapter?
+   3. Write the code to bind a first name label to a DataSet called CustomersDataSet. The form uses CustomersBindingSource. Display the First-Name field from the Customer table.

# Your Hands-On Programming Example

Create a multiple-tier project to obtain data from the employee table in the Pubs database using a stored procedure. Use an ORDER BY clause in the stored procedure to sort the data in order by last name. Display the full employee names (last name, first name, and middle initial) in alphabetical order in a combo box. Do not display the first and last name fields other than in the combo box. Show the remaining fields in text boxes for the selected record, with meaningful identifying labels. Do not include a navigation toolbar. Include a File / Exit menu item to terminate the program.

# Planning the Project

Sketch a form (Figure 3.30) that your users sign off as meeting their needs.

# Figure 3.30

A planning sketch for the hands-on programming example.

![](bbox=[0.12, 0.68, 0.64, 0.84])

Plan the Objects, Properties, and Methods Plan the two tiers. Determine the objects and property settings for the form and its controls and for the data-tier component. Figure 3.31 shows a diagram of the components in the two tiers.

# Presentation Tier

| Object | Property | Setting |
|---|---|---|
| EmployeeForm | Name | EmployeeForm |
|  | Text | Employees |
| FullNameComboBox | Name | FullNameComboBox |
| Text boxes for all database fields (including Hire Date) |  |  |