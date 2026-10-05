Chapter 15    How to work with interfaces and generics

# # Exercise 15-1 Implement the IClone interface

In this exercise, you'll create an application that includes a Customer class that implements the IClone interface. This application creates a List<> that contains clones of a pre-defined Customer object and displays the cloned customers in a list box as shown below. To make this application easier to develop, we'll give you the starting form and classes.

The design of the Clone Customer form

![](bbox=[0.145, 0.263, 0.598, 0.493])

Development procedure

+   1. Open the application in the C:\C# 2010\15\CloneCustomer directory.
2. Display the code for the form, and notice that the Load event handler creates a Customer object, stores it in a variable named customer, and displays the customer in the label at the top of the form.
3. Modify the Customer class so it implements the ICloneable interface.
4. Add an event handler for the Click event of the Clone button. This event handler should use the methods in the Validator class to check the value in the Copies text box to be sure it's present and also an integer. Then, it should create a List<> object that contains the required number of clones of the Customer object. Finally, it should display the cloned customers in the list box.
5. Run the application and test it to make sure it works properly.

487