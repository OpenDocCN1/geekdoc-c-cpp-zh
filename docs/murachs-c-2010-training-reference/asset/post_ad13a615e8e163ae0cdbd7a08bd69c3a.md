
# The code for the Add/Modify Customer form

```sharp
private bool IsValidData() {
    return
        Validator.IsPresent(txtName) &&
        Validator.IsPresent(txtAddress) &&
        Validator.IsPresent(txtCity) &&
        Validator.IsPresent(cboStates) &&
        Validator.IsPresent(txtZipCode);
}
private void PutCustomerData(Customer customer) {
    customer.Name = txtName.Text;
    customer.Address = txtAddress.Text;
    customer.City = txtCity.Text;
    customer.State = cboStates.SelectedValue.ToString();
    customer.ZipCode = txtZipCode.Text;
}
```

# Perspective

In this chapter, you were introduced to another way to develop database applications. Instead of using data sources and datasets, you learned how to use code to create and work with connections, commands, and data readers. When you work this way, your code has to do all of the functions that are done by the table adapter when you use data sources and datasets. This means that you have to write more code, but it also means that you have complete control over how the data is processed.

# Terms

- parameter
- parameterized query
- named variable
- scalar value
- aggregate value
- action query

# Exercise 20-1 Build the Customer Maintenance application

For this exercise, you'll develop the Customer Maintenance application presented in figure 20-8. To make that easier for you to do, we'll give you the two forms for the project as well as the business classes and the Validator class. That way, you'll just need to create the database classes.

# Review the application

1. Open the application in the C:\C# 2010\Chapter 20\CustomerMaintenance directory and review the code for the forms and classes. Notice that some of the statements in the forms have been commented out. These are the statements that call the methods of the database classes that you'll create.

2. Run the application, enter 27 in the Customer ID text box, and click the Get Customer button. When you do, an error message will be displayed indicating that the customer wasn't found. That's because the application doesn't include the code to retrieve the customer. Respond to the dialog box and then end the application.

# Write the code to retrieve a customer

3. Add a class named MMABooksDB to the project. Then, add a method named GetConnection to this class, and add code like shown in figure 20-11 to this method. For this to work, you'll also need to add a using statement for the System.Data.SqlClient namespace at the beginning of the class.

# Chapter 20 How to use ADO.NET to write your data access code 657

4. Add another class named CustomerDB to the project, and add using statements for the System.Data and System.Data.SqlClient namespaces to this class.

5. Add a method named GetCustomer to the CustomerDB class. This method should receive the Customer ID of the customer to be retrieved, and it should return a Customer object for that customer. Add the code for this method as shown in part 1 of figure 20-10, but try to do that without looking at this figure.

6. Display the code for the Customer Maintenance form, and remove the comment from the statement in the GetCustomer method that calls the GetCustomer method of the CustomerDB class. Then, run the application and try to display the data for customer number 27. If this doesn't work, modify your code until it does.

7. Click the Modify button to display the Modify Customer form, and notice that no value is displayed in the State combo box. Drop-down the combo box list to see it contains any items. That's because you haven't added the code to retrieve the list of states. Click the Cancel button to return to the Customer Maintenance form and then end the application.

# Write the code to retrieve the list of states

8. Add a class named StateDB to the project, and add using statement for the System.Data.SqlClient namespace to this class.

9. Add a method named GetStates to the StateDB class. This method should return a List<> of State objects. Add the code for this method as shown in figure 20-11, but again, try to do that without looking at this figure.

10. Display the code for the Add/Modify Customer form, and remove the comment from the statement in the LoadStateComboBox method that calls the GetStates method. Then, run the application, display the data for customer number 27, and click the Modify button. This time, the correct state should be displayed for the customer and the State combo box should be populated with a list of all the states. However, you still't modify the data for the customer because you haven't added the code to do that. Cancel out of the Modify Customer form and then end the application.

# Write the code to modify a customer

11. Add a method named UpdateCustomer to the CustomerDB class. This method should receive two Customer objects. The first one should contain the original customer data and should be used to provide for optimistic concurrency. The second one should contain the new customer data and should be used to update the customer row. This method should also return a Boolean value that indicates the update was successful. Add the code for this method using figure 20-10 as a guide if necessary.

12. Display the code for the Add/Modify Customer form, remove the comments from the statement in the event handler for the Click event of the Accept button. Then, run the application, retrieve 27, click the Modify button, and make a change. If you coded it correctly, the updated data should be displayed on the Customer Maintenance form. Otherwise, you'll need to correct the code.

# Write the code to add a customer

13. Add a method named AddCustomer to the CustomerDB class. This method should receive a Customer object with the data for the new customer, and it should return an integer with the new customer. Add the code for this method using figure 20-10 as a guide if necessary.

14. Display the code for the Add/Modify Customer form, and remove the comment from the statement that calls the AddCustomer method. Then, run the application and click the Add button to display the Customer form.

15. Enter the data for a new customer. Then, click the Accept button to add the customer to the database and display the customer data on the Customer Maintenance form. Note the customer ID for the new customer. When you have this correctly, end the application.

# Write the code to delete a customer

16. Add a method DeleteCustomer to the CustomerDB class. This method should receive a Customer object with the data for the customer to be deleted, and it should return a Boolean value that indicates if the delete operation was successful. The Customer object should be used to provide for optimistic concurrency. Add the code for this method using figure 20-10 as a guide if necessary.

17. Display the code for the Customer Maintenance form, and remove the comments from the statement in the event handler for the Click event of the Delete button. Then, run the application and retrieve the customer you added in step 15.

18. Click the Delete button to see the message that was displayed. Then, click the Yes button to delete the customer. If this worked correctly, the data should be cleared from the Customer Maintenance form and the Modify and Delete buttons should be disabled. When you have this correctly, end the application and close the project.

# Section 5

# Other skills for C# developers

This section contains four chapters that present some skills you may need as you develop Windows applications in C#. Since you won't need them for all your applications, though, you can give these chapters a quick reading just to find out skills they offer. Then, you can return to these chapters for reference whenever you need the skills.

In chapter 21, you'll learn how to read and write the data in two of the file types that are supported by .NET: text files and binary files. In chapter 22, you'll learn how to read and write the data in XML files, which will also prepare you for using XML in other contexts. In chapter 23, you'll learn how to use LINQ to work with objects such as arrays and collections. In chapter 24, you'll learn how to enhance a Windows application by using the multi-document interface and by adding features like menus, toolbars, and help to your forms. And in chapter 25, you'll learn about three ways to deploy a Windows application.
