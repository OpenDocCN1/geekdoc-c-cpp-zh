# Exercise 7-1 Enhance the Invoice Total application

This exercise guides you through the process of enhancing the Invoice application so it catches any runtime errors and validates the Subtotal entry.

+   1. Open the application that's in the C:\C# 2010\Chapter 07\InvoiceTotal directory. This is the version that you worked on in chapter 4.

+   2. Add a try-catch statement to the btnCalculate_Click method so it catches any exception that the ToDecimal method of the Convert class might throw. The catch block should display a dialog box like the one in figure 7-2. Then, test the application to make sure this works correctly.

+   3. Add code to the try block that checks that the user enters a value in the Subtotal box. If a value isn't entered, a dialog box should be displayed with a message indicating that Subtotal is a required field. Then, test this enhancement.

+   4. Add code to the try block that range checks the user entry so it's greater than zero and less than 10,000. If it isn't, a dialog box should be displayed that specifies the acceptable range. Then, test this enhancement. When you're satisfied that the application works correctly, close it.