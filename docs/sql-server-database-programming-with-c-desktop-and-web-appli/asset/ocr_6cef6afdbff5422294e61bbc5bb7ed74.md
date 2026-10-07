# Introduction to Language Integrated Query (LINQ)

In general, we recommend query syntax because it is usually simpler and more readable; however, there is no semantic difference between method syntax and query syntax. In addition, some queries, such as those that retrieve the number of elements matching a specified condition, or the element that has the maximum value in a source sequence, can only be expressed as method calls. The reference documentation for Query Operators in the System.Linq namespace generally uses method syntax. Therefore, when writing LINQ queries, it is useful to be familiar with method syntax in and query expressions themselves.

We have discussed the Standard Query Operator with a few examples of using the method syntax in Sections 4.1.3 and 4.1.4. Refer to those sections to get a clear picture on how to create and use method syntax to perform call LINQ queries. In this section, we give an example to illustrate the different format is the query syntax and the method syntax for a given data source.

Create a new C# project named QueryMethodSyntax. Open the window of the C#Program.cs and enter the code that are shown in Figure 4.34 into this file to replace all original.

FIGURE 4.34 The codes for the example query QueryMethodSyntax.