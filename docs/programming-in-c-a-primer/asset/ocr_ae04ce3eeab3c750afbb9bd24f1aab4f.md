# Creating and Running the Website2 Web-based Application

The Website2 application allows a user to enter a name and select a city. When the user clicks a button, the entered values are displayed. We can run the Website2 Web-based application in the same way as we have run the Website1 Web based application using the F5 key.

# Creating the Website2 Web-based Application

Website2 Web-based application is also an ASP.NET Web site that contains a single page Default.aspx page. This is a web application in C# using ASP.NET and uses labels, button, textbox, dropdownlist controls. The form validates if the name and the city are inputted. If the user has entered the required information, the program displays it on the same page. To create the Website2 Web-based application:

+   - Create the Default.aspx page.
+   - Add code to Default.aspx page.

# Creating the Default.aspx Page

The Default.aspx page allows a user to enter a name and select a city. After the user clicks a button, the entered values are displayed in the Default.aspx page. To create the Default.aspx page:

+   1. Open the Microsoft Visual Studio IDE.
+   2. Select File -> New -> Website to display the New Web Site dialog box.
+   3. By default, the ASP.NET Web Site template appears selected with C:\Documents and Settings\Administrator\My Documents\... To specify the location and name for the Web based application. You can change the name of the Web-based application as per requirement.
+   4. Accept the default settings and click OK to close the New Web Site dialog box. The Microsoft Visual Studio IDE appears with the Source view of the Default.aspx page for the Website2 Web-based application.
+   5. Change the value of the title HTML element to ASP.NET with C# (Form and Controls).
+   6. Click the Design tab to display the Design view for the Default.aspx page.
+   7. Add three Label controls to the Default.aspx page.
+   8. Select the first Label control, which you have added to the Default.aspx page and change the ForeColor property of the control, using the Properties window.
+   9. Change the value of Text property for the first Label control to This is an example of simple form validation in ASP.NET and C# using the Properties window.
+   10. Expand the Font node in the Properties window to display the Bold option.
+   11. Click the editable text box that appears next to the Bold option - display a list with two values True and False.
+   12. Select the True value from the list to make the text appearing in the first Label control as bold.
+   13. Select the second Label control added to the Default.aspx page and change its Text property to Enter your Name.
+   14. Select the third Label control added to the Default.aspx page and change its Text property to Select your City.
+   15. Add a TextBox control to the Default.aspx page using the Toolbox.
+   16. Add a DropDownList control to the Default.aspx page using the Toolbox.