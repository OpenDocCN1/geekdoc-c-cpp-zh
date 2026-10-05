from (referencing the data in the collection in the from clause) to the left of the equals operator and the item you are joining with (referencing the data in the collection in the join clause) to the right.

LINQ provides numerous other methods for summarizing information and joining, grouping, and searching through data. This section has covered just the most common features. For example, LINQ provides the Intersect and Union methods, which you can use to perform set-wide operations. It also provides methods such as Any and All that you can use to determine whether at least one item in a collection or every item in a collection matches a specified predicate. You can partition the variables in an enumerable collection using the Take and Skip methods. For more information, see the material in the LINQ section of the documentation provided with Visual Studio 2022.

# Querying data in Tree<T> objects

The examples you've seen so far in this chapter have shown how to query the data in an array. You can use the same techniques for any collection class that implements the IEnumerable<T> interface. In the following exercise, you'll define a new class for modeling employees for a company. You'll create a BinaryTree object containing a collection of Employee objects, and then you'll use LINQ to query this information. You will initially call the LINQ extension methods directly, but then you will modify your code to use query operators.

> To retrieve data from a BinaryTree by using the extension methods

+   1. Start Visual Studio 2022, if it is not already running.

+   2. Open the QueryBinaryTree solution, which is located in the \Microsoft Press\VCSABS\Chapter 21\QueryBinaryTree folder in your Documents folder.

The project in the solution contains the Program.cs file, which defines the Program class with the Main and doWork methods that you've seen in previous exercises. The solution also includes a copy of the BinaryTree project that you've seen in previous chapters.