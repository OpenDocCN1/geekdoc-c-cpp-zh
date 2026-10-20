# The code for the form

Figure 22-11 shows the code that’s used to implement the paging with EF. To start, this code declares some class-level variables and a constant. The constant named MaxRows indicates the maximum number of rows to be displayed on a page. The variable named totalRows stores the total number of rows. And the variable named pages stores the total number of pages.

The Load event handler for the form starts by using the Count() method of the Customers entity collection to get the total number of rows. Then, it calculates the number of pages. To do that, it divides the total number of rows by the maximum number of rows per page. Then, it uses the modulus operator to check whether there are any remaining rows after the division operation. If so, it adds one to the number of pages.

After these calculations, this code displays the total number of pages in the label to the right of the text box. Then, the Load event handler ends by calling the DisplayCustomers() method and passing it a value of 1 to display the first page of customer rows.

The DisplayCustomers() method begins by displaying the current page number in the text box on the form. Then, it calculates the values for the variables named skip and take. The skip variable stores the number of rows to be skipped before rows are retrieved, and the take variable stores the number of rows to be retrieved for a specific page.

To calculate the take variable, the code begins by setting it equal to the MaxRows constant. In most cases, this is the correct value for the take variable since it displays a full page of rows. However, if the page number is equal to the total number of pages, the code sets the take variable equal to the total number of rows minus the skip variable. That’s because the last page might not have a full page of rows. Similarly, if the total number of rows is less than or equal to the maximum number of rows for a page, this code sets the take variable to the totalRows variable. That’s because the first page doesn’t display a full page of rows in this case.

After calculating the take variable, this code uses a LINQ query to get the customers to be displayed. To do that, this code passes the skip and take variables to the Skip() and Take() methods. Then, it retrieves the entities, converts them to a list, and uses that list as the data source for the grid.

After setting the data source for the grid, this code formats the grid so it appears as shown in the previous figure. To do that, it uses the same techniques used by the Product Maintenance application presented in figure 22-9.

The DisplayCustomers() method finishes by passing its pageNumber parameter to the EnableDisableButtons() method. This enables or disables the buttons on the form depending on the page number.