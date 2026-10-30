# Programming Exercises

+   8.1 Create a Web site that displays the Products table in the Northwind database. Use a DetailsView with pagination.
+   8.2 Modify Exercise 8.1 to retrieve the data from a WCF Service.
+   8.3 Modify Exercise 8.1 or 8.2 to allow the user to update the data in the products table. Hint: The products table has constraints. Include error handling as shown on page 379.
+   8.4 Create a Web site that displays the book information from the RnR Books database. Use a drop-down list for selecting the title and a DetailsView for all the fields.
+   8.5 Modify Exercise 8.4 to allow updates to the data in the books table.
+   8.6 Modify Exercise 8.4 or 8.5 to use a WCF Service for the database.
+   8.7 Create a Web site that allows the user to display customer and order information from the Northwind database. When the user selects a customer name from a list, the rest of the information about the customer should display. Include a link called Orders to a second page that displays a grid of orders for the selected customer.
+   8.8 Display the Suppliers table from the Northwind database in a data grid. Allow the grid to be sorted by Supplier ID, Company Name, or Postal Code and Country. Include pagination. Select a formatting style for the grid and use appropriate headers for the columns; that is, use Supplier ID with a space, not the default SupplierID.
+   8.9 Using the Ch08ShoppingCart project from the text Web site, add the code to insert the customer information into the database. In Server Explorer, create a table called OnlinePurchase with the fields on the customer page.

# Case Studies

# Claytor's Cottages

Complete the Reservations function of the Web site for Claytor's Cottages. Display the room information. Allow the user to enter his or her name, phone number, credit card type, card number, expiration date, room, arrival date, and the number of days.

Optional: Enter arrival and departure dates using a Calendar control.
Challenge: Validate that the days are available.

# Christian's Car Rentals

Complete the Reservations function of the Web site for Christian's Car Rentals. The user must select the size of car and enter the number of days, his or her name, phone number, and credit card information (card type, number, and expiration date).
Generate a string Confirmation ID, which is used as the primary key in the reservation table.

Optional: Enter pickup and drop-off dates using a MonthCalendar control.
Challenge: Validate that there are vehicles remaining in the size category assuming that the company has 20 in each category.
Use a service for the database access.