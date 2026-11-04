> > **NOTE** *You can declare your own nullable variables by following their data types with a question mark. For example, the following code declares a nullable integer variable named numCourses and assigns it the initial value null:*

```
    int? numCourses = null;
```

Databases often have fields that are allowed to have no value and the LINQ to SQL classes represent them as nullable properties. In the database’s Customers table, the Balance and DueDate fields are not required so the customer LINQ to SQL class makes its Balance and DueDate fields nullable. That means when the program’s C# code looks at those fields, they may not contain any value.

To decide whether a field contains a value, you can compare it to null or use its HasValue property. Once you know that the value exists, you can use its Value property to get the value.

For example, the following code checks whether a Customer’s Balance field is null and, if the value exists, displays it:

```
    if (cust.Balance != null)
    {
        // There is a Balance. Display it.
        MessageBox.Show("Balance: " + cust.Balance.Value.ToString());
    }
```

# ## UNDERSTANDING QUERY EXECUTION

Although LINQ to SQL looks a lot like LINQ to Objects in your C# code, behind the scenes there is a huge difference in the way the two kinds of queries are executed.

The C# compiler converts a LINQ to Objects query into a series of method calls to do all of the work. The code does nothing that you couldn’t do yourself in C# code, so it works more or less the way you would expect C# code to work.

In contrast, the compiler converts a LINQ to SQL query into code that can execute within the database. Instead of executing code within your program, it sends commands to the database to make it do all of the work. With a bit of effort, you could come up with similar database commands yourself and make your program execute them on the database, but LINQ to SQL does that for you.

Why should LINQ to SQL handle this differently?

Suppose you want to find a customer with a particular name in a customers array that holds 100,000 objects. LINQ to Objects can zip through the array fairly quickly and find the right customer with little problem.

Now suppose you want to find the same customer in a database containing 100,000 records. To perform that search in C# code, the program would need to fetch 100,000 records from the database. Moving that much data from the database into the program would take quite a bit of time