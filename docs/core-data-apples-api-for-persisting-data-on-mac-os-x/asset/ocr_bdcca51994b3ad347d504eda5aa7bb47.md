to the text field or table column and define its display. Likewise, when working with dates, use an NSDateFormatter on the field or column to ensure that the data will be formatted and validated correctly before it is stored in the Core Data repository. When working with Core Data, it is sometimes necessary to manipulate the display of the data both so that the user's input can be validated and so that it can be displayed in a usable form. For instance, it is not a very good user experience to display currency as 3.99 rather than $3.99 or to display a date in raw seconds.

In our application, we used an NSNumberFormatter to display the quantity in the ingredients column of our second NSTableView. If we were to add a shopping list to our application, we would also use NSNumberFormatter objects to display currency and NSDateFormatter objects to show date and time information.

To add an NSFormatter to a field (either a column or a text field), select it in the library palette, and drag it onto the interface element. Once it is in place, you can configure its details in the Attributes inspector, as shown in Figure 3.3, on the next page. The Attributes inspector will allow you to configure exactly how the data is presented to the user.

In addition to properly displaying number and date data, the NSFormatter classes will also accept input from the user and send it back to the model in the correct format. For example, by applying NSNumberFormatter to the quantity column of the ingredients table, we are guaranteed to receive an NSNumber back from the user interface.

Once an NSFormatter has been applied to an object, it can be a little tricky to reference it again to make changes. To be able to change or remove an NSFormatter once it has been applied, you can select the user interface element, and a small double bracket icon will appear below it. Selecting that icon will reference the NSFormatter again so that it can be manipulated. See Figure 3.4, on page 46.

# ### 3.4 Other Interface Elements That Use KVO, KVC, and Core Data

Although the previous list shows how we are using KVO and KVC to access our Core Data repository in our recipe application, we should quickly review the other elements that, if we wanted or needed to, could be utilized to display the data in our application as well.