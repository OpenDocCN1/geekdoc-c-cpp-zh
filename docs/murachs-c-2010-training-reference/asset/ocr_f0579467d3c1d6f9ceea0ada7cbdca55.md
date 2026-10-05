# Exercise 12-1 Create a Customer Maintenance application that uses classes

In this exercise, you'll create a Customer Maintenance application that uses three classes. To make this application easier to develop, we'll give you the starting forms, a complete Validator class, and a complete CustomerDB class that you'll use to work with the data in a file of customers. Note that the CustomerDB class assumes the file of customers (Customers.txt) is in the C:\2010\Files directory. If you placed this file in a different directory after downloading and installing the files for this book, you will need to change the path specification in the CustomerDB class.

Open the project and add a C# class

+   1. Open the application in the C#2010\CustomerMaintenance directory. Then, review both of the forms in the Form Designer window so you get an idea of how this project should work.
2. Add a class named Customer to this project, and add the properties, method, and constructors that are shown in the table.

| Property | Description |
| --- | --- |
| FirstName | Gets or sets a string that contains the customer's first name. |
| LastName | Gets or sets a string that contains the customer's last name. |
| Email | Gets or sets a string that contains the customer's email address. |

| Method | Description |
| --- | --- |
| GetDisplayText() | Returns a string that contains the customer's name and email address formatted like this: Joanne Smith, jsmith@armaco.com. |

| Constructor | Description |
| --- | --- |
| () (firstName, lastName, email) | Creates a Customer object with default values. Creates a Customer object using the specified values. |

+   3. When you complete the Customer class, jump to the Class View window to review the members for one or more of the members. Then, review the members for the Validator class. Note that one of the methods is IsValidEmail, which you can use to validate email addresses.
4. If you're not using the Express Edition of C#2010, create a class diagram and use it to review the members and code of the Customer and Validator classes as described in step 3.

Add code to implement the Add Customer form

+   5. Display the code for the Add Customer form, and declare a class variable named customer of type Customer with an initial value of null.
6. Add a public method named GetCustomer that displays the form as a dialog box and returns a Customer object.