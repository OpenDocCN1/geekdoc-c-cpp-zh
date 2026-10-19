
Figure 11-16: Menus on ProductsMain form

![](img/143bad48262566137acc9c41f668a88f_347_0.png)

![](img/143bad48262566137acc9c41f668a88f_347_1.png)

Step 2-12: Add the MenuStrip object from the Menus and Toolbars group on the Toolbox. You will see the object in the component tray. Change the name of the MenuStrip from menuStrip1 to MainMenu.

Step 2-13: Click on MainMenu in the component tray. The Menu Designer is displayed at the top of the form with the Type Here field, as shown in Figure 11-17.

Figure 11-17: The Menu Designer

![](img/143bad48262566137acc9c41f668a88f_347_2.png)

Step 2-14: Type File in the Type Here field. This creates a new menu item of the type ToolStripMenuItem. Change the Text property to &File to make “F” the access key for this menu. That means you can press Alt+F to access this menu.

Step 2-15: Type Exit in the Type Here field in the dropdown menu below File. Because we add code to the Click event handler of this menu item, change its name to mnuExit to make it more meaningful. For the ShortCutKeys property, select Ctrl and x. That means pressing Ctrl+x will have the same effect as selecting this menu item.

### Adding Code to the Click Event Handler of Menu Items

Each menu item acts like a button. You can add code to the Click event handlers of the menu items.

Step 2-16: Double click Exit menu item to open the Click event handler. For code, type this.Close();

Next, you create the second menu, Open, and its dropdown menu with two options: Look Up Price and Display Products.

Step 2-17: Type Open in the Type Here field. In the Text property, change the Text to &Open to make “O” the access key for this menu. That means you can press Alt+O to access this menu.

Step 2-18: Type Look Up Price in the Type Here field in the dropdown menu below Open. Because we add code to the Click event handler of this menu item, change its name to mnuLookUpPrice. For the ShortCutKeys property, select Ctrl and L. That means pressing Ctrl+L will have the same effect as selecting this menu item.

Step 2-19: Type Display Products in the Type Here field below Look Up Price. Change the name of the menu item to mnuDisplayProducts. Set Ctrl+D as the ShortCut for this menu item.

When you have different groups of menu items, you may add a separator between groups by selecting it from the dropdown menu of the Type Here field, as shown in Figure 11-18:

Figure 11-18: Menu with a separator

![](img/143bad48262566137acc9c41f668a88f_348_0.png)

### Adding Code to the Click Event Handlers of the Menu Items Look Up Price and Display Products

Note that the menu item mnuLookUpPrice and the button btnLookUpPrice perform the same function of opening the form, LookUpPrice. So, rather than duplicating the code in the Click event handlers of both the button and the menu, we will create a method named LookUpPrice() and call it from both event handlers.

### Calling Event Handlers

You may wonder, why not call the Click event handler btnLookUp_Click directly from the Click event handler mnuLookUpPrice_Click, instead of creating a new method and calling it from both event handlers? This is not desirable because if future changes in the user interface require deleting the btnLookUp button, the menu won’t work. In general, calling event handlers from other programs makes maintenance more difficult.

Step 2-20: Create a method named OpenLookUpPrice(), and call it from the Click event handler of the menu item, mnuLookUpPrice, as shown in Figure 11-19:

Figure 11-19: The OpenLookUpPrice method

```
private void OpenLookUpPrice()
{
    LookUpPrice lookUpPrice = new LookUpPrice();
    lookUpPrice.Show();
}
private void mnuLookUpPrice_Click(object sender, EventArgs e)
{
    OpenLookUpPrice();
}
```

Step 2-21: Delete the code from the Click event handler of btnLookUpPrice and add the code to call the OpenLookUpPrice method, as shown in Figure 11-20:

Figure 11-20: The modified event handler

```
private void btnLookUp_Click(object sender, EventArgs e)
{
    // Modified code:
    OpenLookUpPrice();
}
```

### Submenus

You may create a submenu for a menu item like Display Products by typing the submenu item in the Type Here field displayed to the right.

### Checked Menu Items

A checked menu item has a CheckBox next to it. When the user clicks the menu item, the CheckBox alternates between the states checked and unchecked. To create a checked menu item, set the Checked property of a standard menu item to True.

A checked menu item may be used for on/off type of actions, like hiding and unhiding a control, and to indicate which item is selected from a group of menu items.

You may add code to the Click event handler of a checked menu item just like any other event handler.

It’s time to practice! Do Exercise 11-2.

### Context Menus

Typically, a context menu is associated with a control, and it is displayed by right clicking the control. For example, right clicking a TextBox at runtime displays its standard context menu items, like undo, cut, copy, and paste.

## Review Question

11.7 Different methods that can be used to let the user perform a task in a C# form include (1) clicking a standard button, (2) selecting an item from a standard top-level menu (main menu), (3) selecting an item from a Context menu, and (4) clicking a button on a custom Toolbar.

Consider a form that allows the user to perform different tasks associated with processing payroll (compute pay, deductions, etc.) and save the data. These tasks are performed by clicking standard buttons on the form. In addition, it is desired to let the user change the appearance (color and font size) of a ListBox on the form.

Which one of the above methods is appropriate to let the user change the back color and/or the font size of the ListBox?

## Exercises

### Exercise 11-1

Create the form DisplayProducts, shown in Figure 11-25. Create a Dictionary in this form, and call LoadDictionary method to load the Dictionary with data. Use the Dictionary to display all products with price below the specified limit.

Figure 11-25: The Display Products form

![](img/143bad48262566137acc9c41f668a88f_353_0.png)

### Exercise 11-2

Create a new method named OpenDisplayProducts to open the DisplayProducts form in Ch11_MultiformApps2. Call this method from the Click event handlers of btnDisplayProducts button and mnuDisplayProducts menu item.

### Exercise 11-3

Add another menu item, ForeColor, to the Context menu on the DisplayProducts form to let the user change the ForeColor of the ListBox

Figure 12-1: Relationship between database tables, data table and controls on a form

![](img/143bad48262566137acc9c41f668a88f_355_0.png)

We will use the wizard to create the necessary objects and to help you work with the data.

## 12.2 Creating Database Objects

To create the database object, first, you specify the data source—that is, the source of data, its type and location. The data source could be a database on the local computer or on a server, or a web service or other object.

Next, you drag the data table to the form to create the controls that display the data and objects that bind the controls to the data table.

### Specifying the Data Source

You specify the data source using the Data Source Configuration Wizard, which in turn generates the data tables and other objects, like the binding source.

### Tutorial 1: Display Employee Records Using the Wizard

Let’s create an application that lets you work with a human resource database that includes an Employee table.

Step 1-1: Create a new project named Ch12_Databases. Rename the form to EmployeeTabularView.

Step 1-2: Copy the SQL Server database file HR.mdf from Tutorial_Starts/DataFiles folder to a local directory outside the project directory, Ch12_Database. Appendix B provides instructions on how to create a new database in Visual Studio.

Step 1-3: To start the Data Source Configuration Wizard, click Project from the menu, and click Add New Data Source. You will see the Configuration Wizard window, as shown in Figure 12-2.
