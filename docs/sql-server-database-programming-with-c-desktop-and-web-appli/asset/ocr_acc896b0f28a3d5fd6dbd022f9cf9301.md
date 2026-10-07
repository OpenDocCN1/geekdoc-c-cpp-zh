# Introduction to Language Integrated Query (LINQ)

```
List<string> fruits = new List<string> { "apple", "banana", "mango", "orange", "blueberry", "grape", "strawberry" };

var query = from fruit in fruits
    where fruit.Length < 6
    select fruit;
Console.WriteLine(f);
```

**FIGURE 4.69** A sample LINQ to object query.

+   7. A query used for LINQ to Objects, which is represented by a query syntax, is shown in Figure 4.69. Try to convert this query expression to a method's syntax.
8. Illustrate the procedure of creating each entity for each data table in our sample database CSE_DEPT by using the Object Relational Designer, and adding a connection to the selected database using the DataContext class or the derived class from the DataContext class.
9. Explain the difference between the class method and the instance method, and try to illustrate the functionality of an extension method and how to build an extension method by using an example.
10. List three steps of performing the LINQ to DataSet queries.