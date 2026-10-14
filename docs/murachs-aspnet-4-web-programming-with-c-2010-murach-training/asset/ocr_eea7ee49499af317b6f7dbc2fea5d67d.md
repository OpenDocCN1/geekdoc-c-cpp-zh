+   18. Run the application and click the Edit button in the DetailsView control to make sure you have the controls in the EditItem template formatted properly.
+   19. Copy the text boxes, validation controls, and drop-down list you created for the EditItem templates to the InsertItem templates of the same fields. In addition, add a required field validator to the InsertItem template for the Email field, and modify the text box so it’s wider and accommodates a maximum of 25 characters.
+   20. Run the application again and click the New button. The InsertItem template should look just like the EditItem template except that the email field is editable.

# Add code to check for database and concurrency errors

+   21. Add event handlers for the ItemUpdated, ItemDeleted, and ItemInserted events of the DetailsView control. The ItemUpdated and ItemDeleted methods should check for both database and concurrency errors, but the ItemInserted method should check only for database errors. Display an appropriate error message in the label at the bottom of the page if an error is detected. Otherwise, bind the GridView control so it reflects the current data. If you need help, refer to figure 15-11.
+   22. Run the application and test it to make sure it works correctly.

# Exercise 15-2 Format the data in a FormView control

In this exercise, you’ll modify an application that uses a FormView control for maintaining customers. That will give you an idea of the flexible layouts you can create using this control.

+   1. Open the Ch15CustMaintFormView application in the C:\aspnet4_cs directory.
+   2. Run the application, and experiment with it until you understand how it works.
+   3. Display the page in Design view, and select the Edit Templates command from the smart tag menu for the FormView control. The Item template will be displayed with literal text and a label for each field on a separate line.
+   4. Change the text “City:” to “City, State, Zip:”. Then, drag the State label so it follows the City label, and drag the ZipCode label so it follows the State label.
+   5. Exit from Template Editing mode, and display the page in Source view. Locate the Item template that you just modified, enter a comma and a space (&nbsp;) between the City and State labels, and enter a space between the State and ZipCode labels.
+   6. Delete the paragraphs from the Item template with the text “State:” and “Zip Code:”, along with the paragraph that follows each of these paragraphs that previously contained the State and ZipCode labels.
+   7. Run the application to see that the city, state, and zip code are now displayed on a single line when the Item template is displayed.