# 122 SQL Server Database Programming with C#

In Sections 4.1.3 and 4.1.4, we have provided a very detailed discussion of the Standard Query Operators. Now let's give a little more detailed discussion about LINQ to Objects using those Standard Query Operators. We divide this discussion into the following four parts:

+   1) LINQ and Array
2) LINQ and Strings
3) LINQ and File Directories
4) LINQ and Reflection

Let's starts with the first part, LINQ and ArrayList.

# 4.4.1 LINQ and ArrayList

When using LINQ to query non-generic IEnumerable collections as ArrayList, you must explicitly declare the type of the range variable so to reflect the specific type of the objects in the collection. For example, if you have an ArrayList of Student objects, your clause in a query should look like this:

```
var query = from Student s in arrList
```

By specifying the type of the range variable with Student, you are casting each item in the ArrayList to a Student.
The use of an explicitly created range variable in a query is equivalent to calling the Cast<TResult> method. CastResult throws an exception if the specific cast cannot be performed. CastResult and OfType are the two Standard Query Operator methods discussed in Section 4.1.3 and these two methods operate on non-generic IEnumerable collections.
Let's illustrate this with a C# example project named NonGenericLINQ.cs. Open the Visual Studio 2022 and create a new C# Console project going to File | New | Project menu item, then select the C# Console App template and name it NonGenericLINQ, and entering the codes that are shown in Figure 4.25 into the opened code window of C# Program.cs.
Let's have a closer look at this piece of code to see how it works.

+   A. The System.Collections namespace is added first into this project since all non-generic collections are defined in this. In order to use any non-generic collection such as ArrayList, you must declare this namespace in this project before it can be used.
B. A new Student is created with two members and this class is used as a protocol for those objects to be created and added to the ArrayList generic collector.
C. A new instance of the ArrayList arrList is created and initialized by adding four new Student objects.
D. A LINQ query is created with the student range variable type defined as Student by a Cast operator. The filtering condition is that all student objects should be selected as long as their FirstSort' value is greater than 95.
E. A foreach loop is used to pick up all query results by one and assign it to the iteration variable s. Console.WriteLine() method is executed to display each data item, including the student's name and orders.
F. Two code lines allow users to run in the Debugging mode since the Console window cannot keep its status if you are running in the Debugging mode.

Now you can Build and Run the project, the running result should be:

Svetlana Omelchenko: 98
Cesar Garcia: 97