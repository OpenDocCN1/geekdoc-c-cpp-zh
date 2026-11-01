# CHAPTER 5

# Filter Templates

+   ## IN THIS CHAPTER
+   
+   - Filtering with LINQ
+   - Creating a Filter Template
+   - Dynamic LINQ Queries
+   - Building Search Pages with Filter Templates
+   - Filter Template Lookup Rules
+   - Built-in Filter Templates

Search functionality is essential for most database applications. Whether it is a customer browsing the product catalog or a service representative looking up a customer record, users need a fast and convenient mechanism for finding the information they need. For more than a decade now, ASP.NET developers have been using stored procedures to implement data access code in general and search functionality in particular. For each search screen, such as the Customer search page shown in Figure 5.1, one or more stored procedures would be created, each accepting a number of parameters representing the search criteria and executing an appropriate SELECT statement.

Although implementing a simple page using stored procedures is easy, complexity grows exponentially with the number of additional parameters in the search criteria. Consider the Customer search page shown in Figure 5.1. With only 2 search parameters, City and Title, this search page needs to support 3 different combinations of their values—only City, only Title, and both City and Title. This requires placing conditional logic either in the form of IF statements in the stored procedure body or in the form of logical conditions in the WHERE clause of the SELECT statement to handle each of the 3 combinations. With 3 search parameters, the number of combinations jumps to 7; with 4 parameters, it is already 15; and with only 5 parameters, (a very modest number for an advanced search page in a typical application), the number of possible combination is a formidable 31.

The number of possible combinations of parameter values is important for two reasons. On one hand, it directly affects the complexity of the database code developers have to