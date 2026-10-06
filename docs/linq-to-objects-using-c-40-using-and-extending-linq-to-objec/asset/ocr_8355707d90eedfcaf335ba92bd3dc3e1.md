# 44 CHAPTER 3 WRITING BASIC QUERIES

> NOTE The fact that the order of the keywords is different in SQL is unfortunate for those who are SQL masters; however, one very compelling for the difference was to improve the developer experience. The From-Where-Select order allows the editing environment (Visual Studio in this case) to provide full Intellisense support when writing the query. The moment you write the from clause, the properties of that element as you write the where clause. This wouldn't be the case (and isn't in SQL Server's query editing tools) if the C# designers followed the more familiar Select-From-Where ordering.

Most of the query expression syntax needs no explanation for developers experienced with other query syntax, like SQL. Although the order is different than in traditional query languages, each keyword name gives a strong indication as to its function, the exception being the let and into clauses, which are described next.

# Let-Create a Local Variable

Queries can be written with less code duplication by creating a variable to hold the value of an intermediate calculation or the result of a subquery. The let keyword enables you to keep the result of an expression (a value or a subquery) in scope throughout the rest of the query expression being written. Once assigned, the variable cannot be reassigned with another value.

In the following code, a local variable is assigned, called average, that holds the average value for the entire source sequence, calculated once but used in the Select projection on each element:

The let keyword is implemented purely by the compiler, which creates an anonymous type that contains the original range variable (element in the previous example) and the new let variable. The previous query maps directly to the following (compiler translated) method query:

```
var variance = from element in source
let average = source.Average()
select Math.Pow(element - average), 2;
```

```
var variance =
source.Select (
element =
new
```