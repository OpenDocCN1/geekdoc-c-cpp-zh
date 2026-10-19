# Review Question

11.7 Different methods that can be used to let the user perform a task in a C# form include (1) clicking a standard button, (2) selecting an item from a standard top-level menu (main menu), (3) selecting an item from a Context menu, and (4) clicking a button on a custom Toolbar.

Consider a form that allows the user to perform different tasks associated with processing payroll (compute pay, deductions, etc.) and save the data. These tasks are performed by clicking standard buttons on the form. In addition, it is desired to let the user change the appearance (color and font size) of a ListBox on the form.

Which one of the above methods is appropriate to let the user change the back color and/or the font size of the ListBox?

# Exercises

# Exercise 11-1

Create the form DisplayProducts, shown in Figure 11-25. Create a Dictionary in this form, and call LoadDictionary method to load the Dictionary with data. Use the Dictionary to display all products with price below the specified limit.

Figure 11-25: The Display Products form

![](bbox=[0.08, 0.47, 0.46, 0.705])

# Exercise 11-2

Create a new method named OpenDisplayProducts to open the DisplayProducts form in Ch11_MultiformApps2. Call this method from the Click event handlers of btnDisplayProducts button and mnuDisplayProducts menu item.

# Exercise 11-3

Add another menu item, ForeColor, to the Context menu on the DisplayProducts form to let the user change the ForeColor of the ListBox