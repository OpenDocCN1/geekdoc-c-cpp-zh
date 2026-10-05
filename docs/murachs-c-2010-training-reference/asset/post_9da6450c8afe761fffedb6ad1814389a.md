
# Some of the C# keywords for working with LINQ

| Keyword | Description |
|---|---|
| from | identifies the source of data for the query. |
| where | Provides a condition that which elements are retrieved from the data source. |
| orderby | Indicates how the elements are returned by the query are sorted. |
| select | Specifies the content of the returned elements. |
| join | Combines data from two data sources. |

# Advantages of using LINQ

- Makes it easy for you to query a data source by integrating the query language with C#.
- Makes it easy to develop applications that query a data source by providing IntelliSense, compile-time syntax checking, and debugging support.
- Makes it easy for you to query different types of data sources because you use the same basic syntax for each type.
- Makes it easy for you to use objects to work with relational data sources by providing designer tools that create object-relational mappings.

# Description

- Language-Integrated Query (LINQ) provides a set of query operators that are available as keywords for the C# language. You use these keywords to define a query expression that identifies the data you want to retrieve from the data source.
- To use LINQ with a data source, the data source must implement the IEnumerable<T> interface or another interface that implements IEnumerable<T> such as IQueryable<T>. For more information on interfaces, see chapter 15.
- A data source such as an array or array list that supports the non-generic IEnumerable interface can also be used with LINQ.

# Note

- The LINQ operators are implemented as methods of the Enumerable class. Although you can execute these methods directly, you're more likely to use the keywords that are built into the C# language.

![](img/3148667e42d4db35b3d08576aaa1fa01_726_0.png)

# The three stages of a query operation

Figure 23-2 presents the three stages of a query operation and illustrates these stages using an array. The first stage is to get the data source. How do that depends on the type of data source you're working with. For the array shown here, getting the data source means defining an array named numbers and assigning values to its elements. Also, the array contains five integers with the values 0, 1, 2, 3, and 4.

The second stage is to define the query expression. This expression identifies the data source and the data to be retrieved from that data source. The query expression in this figure, for example, retrieves the even integers from the numbers array. It also sorts those integers in descending sequence. (Don't worry if you don't understand the syntax of this query expression. You'll learn how to code query expressions in the topics that follow.)

Notice here that the query expression is stored in a query variable. That's necessary because this query isn't executed when it's defined. Also notice that the query variable isn't declared with an explicit type. Instead, it's given a type implicitly based on the type of elements returned by the query. In this case, because the query returns integers, the query variable is given the type IEnumerable<int>.

For this work, the data source must implement the IEnumerable or IEnumerable<T> interface. If you're not familiar with interfaces, which consist a set of declarations for one or more properties, methods, and events, but they don't provide implementation for those properties, methods, and events. If you want to learn more about interfaces, you can read chapter 15. For the example in this figure, all you need to know is that an array implements the IEnumerable interface.

The third stage of a query operation is to execute the query. To do that, you typically use a foreach statement like the one shown in this figure. Here, each element's returned by the query expression is added to a string variable. Then, after all the elements have been processed, the string is displayed in a message box. As you can see, this message box lists the even numbers from 4 to 0 as defined by the query expression.

By the way, you may have noticed the two tab characters that I included in each line of this example. They're needed to make the dialog box wide enough to accommodate the entire title. Without these characters, the title would be cut off.

When a query is defined and executed as shown here, the process is referred to as deferred execution. In contrast, queries that are executed when they define use immediate execution. Immediate execution typically occurs when a method requires access to the individual elements returned by the query is executed on the query expression. For example, to get a count of the number of elements returned by a query, you can execute the Count method on the query expression. Then, the query will be executed immediately so that the count can be calculated. Although LINQ provides several methods for returning these types of values, you won't learn about them in this book.

# The three stages of query operation

- Get the data source. If the data source is an array, for example, you must declare the array and then assign values to its elements.
- Define the query expression.
- Execute the query to return the results.

# A LINQ query that retrieves data from an array

```
int[] numbers = new int[6];
for (int i = 0; i < numbers.Length; i++)
numbers[i] = i;
```

# A statement that defines the query in numbers

```
var numberList = from number in numbers
where number % 2 == 0
orderby number descending
select number;
```

# Code that executes the query

```
string numberDisplay = "";
foreach (var number in numberList)
numberDisplay += number + "\t\n";
MessageBox.Show(numberDisplay, "Sorted Even Numbers");
```

![](img/3148667e42d4db35b3d08576aaa1fa01_728_0.png)

# Description

- The process described above is called deferred execution because the query isn't executed when it's defined. Instead, it's executed when the application tries to access the individual elements returned by the query, such as when the query is used in a foreach statement.
- If a query isn't executed when it's defined, it's stored in a query variable. In that case, the query variable is implicitly typed as IEnumerable<T> where T is the type of each element. In the example, the numberList variable is assigned the type IEnumerable<int> since the array contains integers.
- If a query requires access to the individual elements by the query expression, immediate execution occurs. This typically happens when an aggregate value, such as the number of elements in the results, is requested.

Figure 23-2 The three stages of a query operation

# How to code a LINQ query

Now that you have a basic understanding of what a LINQ query is, you need to learn the syntax for coding query expressions.

# How to identify the data source for a query

To identify the source of data for a query, you can see the from clause shown in 23-3. As you can see, this clause declares a range variable that will be used to represent an element of the data source, and it names the data source, which must be a collection that implements IEnumerable<T>. It can also declare a type for the range variable, which is usually omitted. If it is omitted, it's determined by the type of elements in the data source.

The first example in this figure shows how to use the from clause with an array named sales. The first statement in this example declares the array and assigns values to its elements. Then, the second statement defines the query expression, which consists of just the from clause and a select clause. This expression is stored in a query variable named salesList. Finally, a foreach statement loops through the values returned by the query and calculates a sum of those values.

At this point, you should realize that a query expression must start with a from clause that identifies the data source. That way, C# knows which rest of the source of data for the query is, and it can help you construct the query based on that. In addition, a query expression must end with either a select clause or a group clause. In the example in this, the select clause simply indicates that array elements should be returned by the query.

Later in this chapter, you'll see that you can use the select clause to return the fields you want from each element of a data source.

The second example in this figure shows how to use the from clause with a generic list of invoices. Here, you can see that the Invoice class consists of a set of auto-implemented properties. Then, the statement that follows creates a list that's based on this class and loads invoices into it using the GetInvoices method of the InvoiceDB class. Note that it's not important for you to know how this method works. All you need to know that it returns a List<Invoice> object. This object is then assigned to a variable named invoiceList.

The next statement defines the query expression, which includes a from clause that identifies invoiceList as the data source. This expression is assigned to a query variable named invoices. Then, this variable is used in a foreach statement to calculate a sum of the InvoiceTotal fields in the invoices.

You have noticed in both of the examples in this figure that the variable's used in the query expression and the variable that's used in the foreach loop have the same name. That makes sense because they both refer to an element in the data source. However, you should know that you don't have
