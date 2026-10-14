
## Perspective

The GridView control is ideal for any application that displays a list of items retrieved from a database, and nearly all applications have that need. It’s also ideal for displaying search results, such as product searches for an online catalog or document searches in an online customer support site. And it’s ideal for maintaining simple tables that consist of just a few columns.

In the next chapter, you’ll build on your knowledge of the GridView control by learning how to use it in combination with the FormView and DetailsView controls. Both are designed to display the details for an item that’s selected from a GridView control or a list control. And the combination of a GridView control and a FormView or DetailsView control can be powerful.

## Terms

- paging
- command field
- edit mode
- template
- field

## Exercise 14-1 Create a Customer List application

In this exercise, you’ll develop a page that displays customers in a GridView control that includes sorting and paging. When you’re done, the page should look like this:

![](img/c024ccf88e28c30c07dd410d4342288f_499_0.png)

### Create the GridView control and the SQL data source

- 1. Open the Ch14CustomerList application in the C:\aspnet4_cs directory. This application contains the starting page and the image and style sheet used by the page.
- 2. Add a GridView control to the main division of the page, and create a data source that retrieves the LastName, FirstName, State, and City columns from the Customers table sorted by LastName.
- 3. Use the AutoFormat dialog box to apply the Simple scheme to the control.
- 4. Use the Fields dialog box to left-align the header for each field and to set the column widths to 175, 150, 75, and 150 respectively.
- 5. Run the application to see how it looks. Notice that all the customers are displayed on a single page.

### Add paging to the GridView control

- 6. Display the smart tag menu for the GridView control and check the Enable Paging option.
- 7. Set the Mode property in the PagerSettings group for the GridView control to NextPreviousFirstLast. In addition, set the BackColor property in the PagerStyle group so the background color of the pager area is the same as the background color of the header.
- 8. Run the application again, and use the paging controls to display different pages.

### Add sorting to the GridView control

- 9. Display the smart tag menu for the GridView control and check the Enable Sorting option.
- 10. Remove the sort expressions from the FirstName and City fields, and set the sort expression for the State field so it sorts by city within state.
- 11. Run the application, and click the State heading. The rows should be sorted by city in ascending sequence within state in ascending sequence. Notice that the color of the sorted column changes.
- 12. Click the State heading again. This time, the rows should be sorted by city in descending sequence within state in ascending sequence, and the column should be displayed in a different color.
- 13. Close the browser, and delete the four Sorted style elements that were added to the GridView control when you applied the scheme. You can also delete any other style elements that aren’t used by this application if you’d like.
- 14. Run the application one more time, and click the State heading. This time, the formatting shouldn’t change. Continue experimenting if you want, and then close the browser.

## Exercise 14-2 Create a Product Receipt application

In this exercise, you’ll create a simple application that uses a GridView control to let the user update the on-hand quantity for products when a shipment is received. That will give you an idea of how to work with command fields and templates.

### Create the GridView control using bound fields

- 1. Open the Ch14ProductReceipt application in the C:\aspnet4_cs directory. This application contains a page with a starting GridView control and its data source, a validation summary control that will be used to display error messages for validation controls you’ll add later in this exercise, and a label that will be used to display database errors.
- 2. Display the Default page in Source view and review the code for the data source that’s used by the GridView control.
- 3. Display the Fields dialog box, and set the ReadOnly property of the Name field to True so this field can’t be changed.
- 4. Add a command field to the GridView control that provides for updating a row.
- 5. Add an event handler for the RowUpdated event of the GridView control. Add code like that shown in figure 14-10 that checks for database exceptions and displays error messages in the label near the bottom of the page. Don’t check for concurrency errors, though, since the data source doesn’t provide for concurrency checking.
- 6. Run the application. Click the Edit button for one of the products, change the on-hand amount, and click the Update button. If this works, click the Edit button again, clear the on-hand amount, and click the Update button. This time, an error message should be displayed indicating that a database error occurred. Click the Cancel button and close the browser.

### Convert a bound field to a template field

- 7. Display the Fields dialog box for the GridView control, highlight the OnHand field, and click the Convert This Field into a Template Field link.
- 8. Display the EditItem template for the OnHand field, give the text box an appropriate name, and change its width to 75.
- 9. Add required field and compare validators after the text box. The compare validator should check that an integer greater than or equal to zero is entered. If an error occurs, display an asterisk in a white font following the text box, and display an error message in the validation summary control at the bottom of the page.
- 10. Run the application, click the Edit button for one of the products, clear the on-hand amount, and click the Update button to see that an asterisk is displayed to the right of the text box and the error message is displayed in the validation summary control. Now, try entering an invalid number to see what happens. When you’re done experimenting, close the browser.

## 15

## How to use the DetailsView and FormView controls

In this chapter, you’ll learn how to use the DetailsView and FormView controls. Although both of these controls are designed to work with the GridView control to display the details of the item selected in that control, they can also be used on their own or in combination with other types of list controls such as drop-down lists or list boxes.

- How to use the DetailsView control ........................................ 484
- An introduction to the DetailsView control .................................... 484
- Attributes and child elements for the DetailsView control ...................... 486
- How to define the fields in a DetailsView control .............................. 486
- How to enable paging ........................................................ 488
- How to create a Master/Detail page ........................................... 490
- How to update DetailsView data .............................................. 492
- An introduction to command buttons ........................................... 492
- How to add command buttons .................................................. 494
- How to use events raised by the DetailsView control ........................... 496
- How to create template fields ................................................ 498
- The Product Maintenance application ....................................... 500
- The operation of the application ............................................. 500
- The aspx file ................................................................ 500
- The code-behind file ......................................................... 504
- How to use the FormView control ............................................ 508
- An introduction to the FormView control ...................................... 508
- How to work with the Item template .......................................... 510
- How to work with the EditItem and InsertItem templates ....................... 512
- A Shopping Cart application that uses a FormView control ..................... 514
- The operation of the application ............................................. 514
- The aspx file for the Order page ............................................. 516
- The code-behind file for the Order page ...................................... 516
- Perspective ................................................................. 520
