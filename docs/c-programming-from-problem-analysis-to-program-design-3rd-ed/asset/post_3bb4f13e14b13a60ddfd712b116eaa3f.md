
- 16. A Calendar control is used to display a monthly calendar on a Web page. After being placed on the page, the calendar is live and users can employ it to view and select dates. To work programmatically with the calendar for the **WebControls** application, you declare an `object` of the `DateTime` class.
- 17. The **DataGrid** and **GridView** controls are very useful for displaying data in a tabular format. To populate these controls, the actual data can come from sources such as arrays or database tables.
- 18. Web services are applications that return unformatted data. Windows Communication Foundation (WCF) can be used to create service oriented applications that communicate over the Internet.
- 19. Using a smaller subset of the .NET Framework, you can design, develop, debug, and deploy applications that run on personal digital assistants (PDAs), mobile phones, and other resource-restricted devices.

## EXERCISES

- 1. .NET Web applications differ from Windows applications in that Web applications must take the following into consideration:
  - a. Multiple users need to be able to access the application at the same time.
  - b. An application must be viewable by multiple types of platforms, including Linux and Windows.
  - c. Fewer graphical user interface controls are available for Web applications.
  - d. A Web server must be loaded for development of Web applications.
  - e. all of the above
- 2. The term *Web application* is synonymous with:
  - a. Web server
  - b. IIS
  - c. Web Forms
  - d. Web page
  - e. Web site
- 3. Interaction with users on Web applications cannot include the use of:
  - a. **MessageBox**
  - b. Label
  - c. TextBox
  - d. ListBox
  - e. Button

- 9. The HTML control property used to set the text on a label is:
  - a. Text
  - b. Name
  - c. InnerText
  - d. ID
  - e. none of the above

- 10. When you set property values for Web Forms controls, the program statements referencing the settings are:
  - a. placed in the code-behind file
  - b. placed in the .aspx.cs file
  - c. stored in the .aspxm file
  - d. stored in the file containing the HTML tags
  - e. none of the above

- 11. The default home directory for storing C# Web applications when IIS is used is:
  - a. C:\\CSharpProjects
  - b. C:\\localhost
  - c. C:\\Inetpub\\wwwroot
  - d. C:\\WebApps
  - e. none of the above

- 12. Events associated with which of the following automatically trigger a postback to the Web server?
  - a. ListBox
  - b. TextBox
  - c. DropDownList
  - d. Button
  - e. all of the above

- 13. Which control is often used to display data from a database table?
  - a. DataGrid
  - b. DataTable
  - c. Table
  - d. DataList
  - e. none of the above

- 14. A file ending with the extension of .aspx is associated with which type of application?
  - a. ASP.NET Web page
  - b. smart device
  - c. Web service
  - d. Windows
  - e. classic ASP

- 15. The validation control used to make sure values have been entered into a field is:
  - a. RangeValidator
  - b. FieldRequiredValidator
  - c. CompareValidator
  - d. RequiredFieldValidator
  - e. Required

- 16. To work programmatically with the Calendar control, instantiate an object of the ______ class.
  - a. Calendar
  - b. DateTime
  - c. Date
  - d. CalendarDate
  - e. none of the above

- 17. Web services are applications that return:
  - a. data
  - b. program statements with value-added logic
  - c. graphical user interfaces
  - d. fully functioning Web applications
  - e. none of the above

- 18. The protocol used to encapsulate method calls (and return results) into XML statements is:
  - a. HTTP
  - b. HTML
  - c. SOAP
  - d. SXML
  - e. WSDL

- 19. A file ending with the extension of .xaml is associated with which type of application?
  - a. WebService
  - b. WebClass
  - c. Web application
  - d. Mobile application
  - e. all of the above

- 20. Master pages also require one or more
  - a. content pages
  - b. server
  - c. Web service
  - d. HTML control
  - e. none of the above

- 21. Describe how the classic or traditional ASP programming model differs from the ASP.NET programming model for creating Web pages.

- 22. How do dynamic pages differ from static pages?

- 23. Compare and contrast HTML controls with Web Forms controls in terms of the code generated and the property values that can be set.

- 24. What is a Web service?

- 25. Identify and describe three types of validation controls that can be added to a Web application.

## Programming Exercises

- 1. The computer club has decided to take a field trip to the hometown of one of the members during spring vacation. To determine the destination, each member has been charged with creating a Web page to highlight the features of his hometown. Create a static Web application that contains details about your hometown. If you would prefer that the members visit another location, you may choose a different locale. Set the properties on the form for the controls so the form is aesthetically pleasing. Be sure to change both background and foreground colors, font size, and type.

- 2. Modify the Web application developed for Exercise 1 to include an HTML server control that causes a message to be displayed (on a Label object) when the user clicks a button. The message should include additional details about the locale.

- 3. Using Web Forms controls, create a Web application to include a TextBox object, a Button object, and a ListBox object. Allow the user to input values into the TextBox. Use those values to populate the ListBox object. Fill the ListBox with names, shopping items, types of secondary storage, or some other items of your choosing. Allow the user to make a selection from the ListBox and display the selection on a Label object.

- 4. Create a dynamic Web site that functions like a calculator. Add features for addition, subtraction, multiplication, division, modulation, and so on. For simplicity, you can use two TextBox objects to accept data input and a Button object to trigger the event.

- 5. Create a Web application that enables the user to enter first name, last name, and e-mail address. Accept those values and store them in a text file. Add validation controls to all three controls to ensure each has a value before loading it to the file. Confirm that the values are written to the file.

- 6. Create a Web application that enables users to select from a Calendar control object the date of their next exams. Using program statements, retrieve their selections and then display the date along with an appropriate message.

- 7. The computer club is selling T-shirts. Create a Web site that allows users to enter their first and last names and to select sizes (S, M, L, XL, and XXL) and quantity. Add statements that process the order by calculating the total cost. Each shirt is $26; the XXL shirt is $30. Display the total cost of the selection including 7% tax.

- 8. The Access Member database used with examples in this book includes a major table that stores the major id, major name, department chair, and the number of faculty in the department. Create a Web site that references this table, or an Access database table that you create with similar fields. Display on the Web site the name of the major and the chair for the department. Allow edits, but not deletions, from the table on the Web site.

- 9. Create a smart device currency converter application. Select two markets, such as U.S. dollar and the Euro. Research the current equivalents and use those values for your calculations.

- 10. Create a smart device application that allows users to input their names and student IDs. Create and display a new identification number. The new ID should consist of the first initial of their names followed by the original identification numbers. Append onto the end of those values the total number of characters in their names. For example, if the name Sofiya ElKomaria and the ID 12467 is entered, the new identification number would be S1246716.
