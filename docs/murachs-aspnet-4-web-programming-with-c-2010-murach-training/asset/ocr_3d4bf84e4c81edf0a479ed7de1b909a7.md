+   7. Press the F10 key to execute the Step Over command. This should step over all statements in the GetSelectedProduct method and enter break mode before the next statement in the Page_Load method is executed.
+   
+   8. Point to the Text property of the labels to display these values. Then, point to the selected product to see the values that are stored in this object. Step through the statements that assign the product properties to the Text property of the labels and note how the values in the Text property change.
+   
+   9. Note the values that are displayed in the Locals window. Click the plus sign next to the form object (this) to expand it and review the information that’s available. When you’re done, click the minus sign to collapse the information for this object.
+   
+   10. Remove the breakpoint from the Page_Load method. Then, set another breakpoint on the statement in the GetSelectedProduct method that sets the value of the selected product’s name, continue execution of the application, and select another product. When the application enters break mode again, notice all the variables that are now displayed in the Locals window. That should include all of the variables that are in scope.
+   
+   11. Display a Watch window. Add the Name column of the DataViewRow object to this window by dragging it from the Code Editor window. In the Watch window, it should look something like this:
+   
+       `row["Name"].ToString()`
+   
+       Then, enter an expression into the Watch 1 window that displays the Count property of the DataView object. In the Watch window, it should look something like this:
+   
+       `productsTable.Count`
+   
+       Note the value of the Count property. It should be 1.
+   
+   12. Enter the same expression into the Immediate window, preceded by a question mark. Press the Enter key to see the value that’s displayed. It should be 1.
+   
+   13. Use the Immediate window to assign a new value to the Name column of the DataViewRow object. Check the value of this property in the Watch window and note that the new value is displayed.
+   
+   14. Press F5 to continue program execution. This should display the Order page. Note that the Name value that you set in the previous step is displayed on the Order page.
+   
+   15. Select another product from the combo box. This should cause the application to enter break mode again.
+   
+   16. Click the Stop Debugging button in the Debug toolbar to end the application. Note that the breakpoint remains in the Code Editor even after you have stopped debugging.

# Exercise 4-2   Use the Trace feature

In this exercise, you’ll use the Trace feature of ASP.NET to display trace output on the Order page of the Shopping Cart application that you created in the exercises for chapter 3.

+   1. If it’s not already open, open the Ch04Cart web site.