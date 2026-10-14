# ## The first page of the Configure Data Source wizard

![](bbox=[0.16, 0.11, 0.85, 0.52])

# ## How to create an Access data source

+   1.  In the Web Forms Designer, open the Data group of the Toolbox and drag the AccessDataSource control to the form.
2.  Select Configure Data Source from the smart tag menu of the data source control to display the Configure Data Source dialog box.
3.  Identify the Access database that you want to use in the App\_Data folder and click Next. Then, complete the Configure Data Source wizard as described in the next figure.

# ## Description

+   -   Before you can create an Access data source, you must add the Access database file to the App\_Data folder.
-   The Shopping Cart application uses an AccessDataSource control to provide the list of products that's displayed in the drop-down list. This control reads data from a Microsoft Access database file.
-   Although data source controls are visible in the Web Forms Designer, they don't render any HTML to the browser. As a result, they aren't visible when the application runs.

Figure 3-10 How to create an Access data source