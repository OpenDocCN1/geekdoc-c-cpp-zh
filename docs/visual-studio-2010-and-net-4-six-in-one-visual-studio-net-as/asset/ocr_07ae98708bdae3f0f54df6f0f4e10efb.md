# AUTO-ENCODING SYNTAX

You may recognize a new %: ... %> syntax element in Listing 18-8 rendering the ViewData["Message"] in its body. This syntax automatically HTML-encodes the expression specified in its body. Automatic encoding is a method that dramatically reduces the risk of cross-site scripting (XSS) vulnerabilities.

This syntax is new in .NET 4. As mentioned earlier in this chapter, ASP.NET MVC 2 can be used with .NET 3.5 (in Visual Studio 2010) and in Visual Studio 2010), but in this case, you cannot use the auto-encoding syntax. You should use the old <%= ... %>.

# ADDING NEW MVC 2 PAGES

The AcmeLibrary application created with the ASP.NET MVC 2 Web Application project template does not provide any real functions. In this section, you add functions to the application that allow you to list and edit books. The application will persist information in a SQL database. The components you create are a great demonstration of MVC's strength. You can establish a clear architecture with short and simple source code.

# Create a Database

The AcmeLibrary application will manage a list of books that are stored in a database. So, first you must create this database and define its structure.

In Solution Explorer, right-click the App_Data folder. In the context menu, select the Add New Item command. When the dialog appears, select the SQL Server Database in the Data category, and set its name to AcmeLibraryData.mdf, as shown in Figure 18-11.

![](bbox=[0.139, 0.653, 0.712, 0.913])

FIGURE 18-11: Adding a new database to the project