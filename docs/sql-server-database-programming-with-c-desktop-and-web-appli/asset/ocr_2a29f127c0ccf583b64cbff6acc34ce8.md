# Data Selection Query with Visual C#.NET

![](bbox=[0.147, 0.083, 0.852, 0.477])

FIGURE 5.39 The result of the TableAdapter configuration wizard.

Before we can begin to do our coding job, we need to bind data to controls on the Login form to setup the connection between each control on the form and each data column on the data source.

# 5.6 BIND DATA TO THE ASSOCIATED CONTROLS IN LOGIN FORM

Open the Solution explorer window and select the Login Form from that, then click the View Designer to open its GUI. Now we want to use the BindingSource to bind controls in the Login form, exactly the User Name and Pass Word TextBoxes, to the associated data fields in the Login table in the data source.

Click on the User Name TextBox, then go to the DataBindings property that is located in the top section of the window. Expand that property to display the individual items, and then select the Text item. Click the drop-down to expand the following items:

+   - Other Data Sources
  Project Data Sources
    CSE DEPTDDataSet
    LogIn
    user_name

The expansion result is shown in Figure 5.40.