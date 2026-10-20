# The code for the Product Maintenance form

Figure 22-9 shows the code for the Product Maintenance form. Because the code for the DB context and entity classes and the Add/Modify Product form works like the code shown in chapter 20, it’s not shown here. However, the download for this book includes the complete code for this application.

This code starts by declaring variables to store the DB context and the selected product. Then, the Load event handler for the form calls the DisplayProducts() method. This method gets the data source for the grid and formats the grid.

To do that, the DisplayProducts() method starts by clearing the grid. That’s because the products need to be redisplayed each time a product is added, modified, or deleted. Then, it gets and sets the data source for the grid. This data source consists of the three columns shown in the previous figure.

After setting the data source, this code adds the two button columns. Then, it sets the font, back color, and fore color of the column headers. Next, it sets the back color of the odd numbered rows. Finally, it sets the header text, widths, alignment, and formatting of the columns.

Page 2 of this listing presents the event handler for the CellClick event of the grid. This event handler is the same as the one shown in figure 22-7, so you shouldn’t have much trouble understanding how it works.

If the user clicks a Modify button, the ModifyProduct() method is executed. This method displays the Add/Modify Product form with the data for the selected customer. Then, if the updated product data is valid (DialogResult.OK), this code gets the data from the form, stores it in the selectedProduct variable, saves the changes to the database, and displays the updated list of products in the grid.

Page 3 of this listing presents the DeleteProduct() method. This method is executed if the user clicks a Delete button. It begins by displaying a dialog box that confirms the delete operation. If the operation is confirmed, this code marks the product as deleted, saves the change to the database, and displays the updated list of products in the grid.

If a concurrency exception occurs during an update or delete operation, the current database values for the product are loaded into the entity. Then, the state of the entity is checked to see if it was updated or deleted. This determines the message that’s displayed. In either case, this code displays the updated list of products in the grid. Since the code for this is the similar to the concurrency code presented in chapter 20, it’s not presented here. However, you can review the code that handles concurrency issues in the book application that’s in the download for this chapter.

If the user clicks the Add button, this code displays a blank Add/Modify Product form. Then, if the product data is valid (DialogResult.OK), this code retrieves the data from the form and stores it in the selectedProduct variable. Then, it adds that product data to the entity collection, saves the new product to the database, and displays an updated list of products in the grid.