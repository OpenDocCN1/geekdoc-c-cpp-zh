# A maintenance application that uses a GridView control

To give you a better idea of how you can use a GridView control to update, delete, and insert data, the following topics present an application that maintains the Categories table in the Halloween database.

# The Category Maintenance application

Figure 14-12 introduces you to the Category Maintenance application. It lets the user update, delete, and insert rows in the Categories table of the Halloween database. Here, a GridView control is used to display the rows in the Categories table along with Edit and Delete buttons. In this figure, the user has clicked the Edit button for the third data row, placing that row in edit mode.

Beneath the GridView control, three text boxes let the user enter data for a new category. Then, if the user clicks the Add New Category button, the data entered in these text boxes is used to add a category row to the database. Although it isn’t apparent from this figure, required field validators are used for each text box. Also, there’s a label control beneath the GridView control that’s used to display error messages when an update, delete, or insert operation fails.