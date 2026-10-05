# Perspective

In this chapter, you learned the basic skills for coding and executing LINQ queries in C#. With these skills, you should be able to create simple queries that work with a variety of objects. However, there’s a lot more to learn about LINQ than what’s presented here.

For example, there are other clauses you can code in a query expression. In addition, there are special techniques you need to learn use LINQ with other data sources, such as untyped datasets and databases. To learn about these features, you can refer to Visual Studio help, or you can get a separate book on LINQ.

# Terms

+   - Language-Integrated Query (LINQ)
object-relational mapping
query operator
query expression
deferred execution
query variable
immediate execution
range variable
projection
anonymous type

# Exercise 23-1 Create the Customer Invoice application

In this exercise, you’ll develop and test the Customer Invoice application that was presented in this chapter that uses generic lists.

# Design the form

+   1. Open the project that’s in the C:\C# 2010\Chapter 23\CustomerInvoices directory. In addition to the Customer Invoice form, this project contains the business and database classes needed by the application.
2. Add a ListView control to the Customer Invoice form, and set the View property of this control to Details.
3. Use the smart tag menu for the ListView control to display the ColumnHeader Collection Editor. Then, define the column headings for this control so they appear like the last three shown in figure 23-8. (You’ll add the first column later).