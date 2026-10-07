# SQL Server Database Programming with C#

SQL query is performed on classes that implement IQuery<T> interface. The relationship between the IEnumerable<T> and the IQuery<T> interfaces is: IQuery<T> implements IEnumerable<T>, in addition to the Standard Query Operator (SQO), the LINQ to SQL queries have additional query operators since it uses the IQuery<T> interface.

# ### 4.1.1 The Enumerable and IEnumerable<T> Interfaces

The IEnumerable<T> interface is a key part of LINQ to Objects and it allows all of the C# 2 generic collection classes to implement it. This interface permits the enumeration of a collection's elements. All of the collections in the System.Generic namespace support the IEnumerable<T> interface. Here T converts the data type of the sequence or collection. For example, if you have an IEnumerable<int> of int, expressed by IEnumerable<int>, it is a sequence or collection of ints.

In the case of the non-generic collections which existed in the old version of C#, such as C 1.0 or older, they do not support the IEnumerable<T> interface because of the stronger property of the type. Therefore, you cannot directly call those SQO methods whose first argument is an IEnumerable<T> using non-generic collections. However, you can perform LINQ queries using these collections by calling the Cast or OffType SQO to generate a sequence that implements IEnumerable<T>.

Here, a coding example of LINQ to Object is shown in Figure 4.1.

The type IEnumerable<int> plays two important roles in this piece of code.

+   1) The query expression has a data source called intArray which implements IEnumerable<int>.
2) The query expression returns an instance of IEnumerable<int>.

Every LINQ to Objects query expression, including the one above, will begin with a line of this type:

From x in y

In each case

The query in Figure 4.1 can be re-written in such a way as is shown in Figure 4.2.
This piece of code makes explicit the type of variable returned by this query, IEnumerable<int>. In practice, you will find that most LINQ to Objects queries return IEnumerable<T>, for different data T.

```
// create an integer array
int[] myArray = new int[] {1, 2, 3, 4, 5 };
IEnumerable<int> intArray = myArray.Select(i => i);
//LINQ query expression
var query = from num in intArray
    where num >= 3
    select num;

foreach (var intResult in query)
{
    Console.WriteLine(intResult);
}
```

Figure 4.1 A coding example of using LINQ to object query.