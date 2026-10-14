# Exercise 17-2 Modify the Product Receipt application

In this exercise, you’ll modify the Product Receipt application you created in exercise 14-2 so it uses an object data source instead of a SQL data source. To make that easier, we’ll include the code for the data access class and the business class that are used by the application.

# Review the starting code

+   1. Open the Ch17ProductReceipt application in the C:\aspnet4_cs directory.
+   2. Review the aspx code for the Default page. Then, run the application to refresh your memory about how it works.
+   3. Review the code for the Product class in the App_Code folder to see that it defines three auto-implemented properties for the ProductID, Name, and OnHand columns.
+   4. Review the code for the ProductDB class. Notice that the GetProducts method returns a List<Product> objects. Also notice that the UpdateProduct method accepts a single Product object since it doesn’t implement optimistic concurrency.

# Add an ObjectDataSource control

+   5. Add an ObjectDataSource control to the Default page, and configure it so it retrieves data using the GetProducts method of the ProductDB class and updates a product using the UpdateProduct method.
+   6. Set the DataObjectTypeName property of the object data source to “Product”.
+   7. Change the data source for the GridView control from the SQL data source to the object data source you just created. When a dialog box is displayed asking if you want to regenerate the GridView column fields and data keys, click No.
+   8. Delete the SqlDataSource control since it’s no longer used by the page.
+   9. Run the application and test it to be sure it works correctly. When you’re done, close the browser window.

# Use the designer to review the bound fields

+   10. Display the smart tag menu for the GridView control and select the Edit Columns command.
+   11. Select the ID field, and scroll through the properties for that field until you can see the DataField property.
+   12. Display the drop-down list for the DataField property, and notice that you can see the names of all the available fields. That’s because the select method returns a strongly-typed List<Product> collection.