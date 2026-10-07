
# Introduction to Language Integrated Query (LINQ)

```csharp
// create an Integer array
int[] myArray = new int[] {1, 2, 3, 4, 5 }; IEnumerable<int> query = from num in myArray
                    where num >= 3
                    select num;

foreach (var intResult in query)
{
    Console.WriteLine(intResult);
}
```

**FIGURE 4.2** A modification of the coding example using LINQ to object query.

By finishing these two, it should be clear that to interfaces IQueryable and IEnumerable<T> play a key role in LINQ to Objects queries. The former is used for the non-generic collections and the latter is used for the generic collections. The point is that a typical LINQ to Objects expression only takes a class that implements IEnumerable<T> as its source, but also returns an instance with the same type.

## 4.1.1.2 The IQueryable and IQueryable<T> Interfaces

As discussed in the previous section, IQueryable and IQueryable<T> are two of the interfaces used for LINQ to SQL queries. Similar to IEnumerable and IQueryable<T> interfaces, where the Standard Query Operator methods are defined as the static members in the Enumerable class, the Standard Query Operator methods for the IQueryable<T> interface are defined as static members of the Queryable class. The IQueryable interface is principally used for the non-generic collections and the IQueryable<T> is used for generic collections. Another point is that the IQueryable<T> interface is inherited from the IEnumerable<T> interface from the Queryable class and the definition of this interface:

```csharp
interface IQueryable<T> : IEnumerable<T>, Queryable
```

From this inheritance, we can treat an IQueryable<T> sequence as an IEnumerable<T> sequence. Figure 4.3 shows an example of using the IQueryable interface to perform query to some database CSE_DEPT. A database connection has been made using the DataContext object before this code can be created. The Login is the name of a table in this database and has it is

```csharp
// create a database connection using the DataContext object
public CSE_DEPTDataContext cse_dept = new CSE_DEPTDataContext();
// create local variables
string username = string.Empty;
string password = string.Empty;
// LINQ query expression
IQueryable<Login> login = from lg in cse_dept.Logins
                            where lg.user_name == txtUserName.Text &&
                            lg.pass_word == txtPassWord.Text
                            select lg;

foreach (log in login)
{
    username = log.user_name;
    password = log.pass_word;
}
```

**FIGURE 4.3** A coding example using LINQ to SQL query.

been been converted to an entity by the LINQ Query Operator, an IQueryable<T> interface, exactly a Standard Query Operator, is utilized to perform this. The Login works as a type in the IQueryable<T> interface to make sure that both the input and returned sequence are strongly typed sequences with the type of Login. The Standard Query Operator fetches and returns the matched sequence and assigns them to the associated string variables using the foreach loop. Now let's have a look at the Standard Query Operator (SQO).

## 4.1.2 STANDARD QUERY OPERATORS

There are two sets of LINQ Standard Query Operators, one that the other operates on objects of type IEnumerable<T>. The methods that make up each set are static members of the Enumerable and Queryable classes, respectively. They are defined as extension methods of the type that they operate on This means they can be called by either static syntax or instance method.

In addition, standard query operator method operates on types other than those based on IEnumerable<T> or IQueryable<T>. The Enumerable type defines two methods that both operate on objects of type IEnumerable. These methods, Cast<T>(IEnumerable) and Type<T>(IEnumerable), allow you to enable a non-parameterized, or non-generic, collection to be queried in LINQ pattern. They do this by creating a strongly typed collection of objects. The Queryable class defines two similar methods, Cast<T>(IQueryable) and Type<T>(IQueryable), which operate on objects of type Queryable.

The standard query operators differ in the manner of their execution, depending on whether they return a single value or a sequence of values. Methods that return a single value (for example, Average and Sum) execute immediately. Methods that return a sequence defer the execution and return an enumerable object.

In the case of the methods that operate on in-memory collections, that is those methods that extend IEnumerable<T>, the returned enumerable object captures the arguments that were passed to the method. When object is executed, the logic of the query operator is employed and the results are returned.

In contrast, methods that extend IQueryable<T> do not implement any querying behavior, but build an expression tree that represents the query to be performed. The query processing is handled by the source IQueryable<T> object.

Calls to methods can be chained in one query, which enables queries to become arbitrarily complex.

According to their functionality, the Standard Query Operators and Non-deferred Standard Query Operators can be divided into two categories: Deferred Standard Query Operators and Immediate Standard Query Operators. Figure 4.4 lists some most often used Standard Query Operators.

Because of the limitations of scope, we will select some often used Standard Query Operators and give a detailed discussion for them one by one.

## 4.1.3 DEFERRED STANDARD QUERY OPERATORS

Both deferred Query Operators and non-deferred operators are organized based on their purpose and we will discuss this based on the purpose.

### AsEnumerable (Conversion Purpose)

The AsEnumerable method has no effect other to change the compile-time type of source that implements IEnumerable<T> to IEnumerable<T>. This means that if an input sequence has a type of IEnumerable, the output sequence will also be converted to one that has the same type. Enumerable.

### Cast (Conversion Purpose)

# Introduction to Language Integrated Query (LINQ)

| Standard Query Operator | Purpose | Deferred |
|---|---|---|
| All | Quantifiers | No |
| Any | Quantifiers | No |
| AsEnumerable | Conversion | Yes |
| Average | Aggregate | No |
| Cast | Conversion | Yes |
| Distinct | Set | Yes |
| ElementAt | Element | No |
| First | Element | No |
| Join | Join | Yes |
| Last | Element | No |
| OType | Conversion | Yes |
| OrderBy | Ordering | Yes |
| Select | Projection | Yes |
| Single | Element | No |
| Sum | Aggregate | No |
| ToArray | Conversion | No |
| ToList | Conversion | No |
| Where | Restriction | Yes |

FIGURE 4.4 Most often used query operators.

```csharp
FacultyDataAdapter.SelectCommand = accCommand;
FacultyDataAdapter.Fill(ds, "Faculty");
var facultyinfo = (from fi in ds.Tables("Faculty").AsEnumerable()
    where fi.Field<string>("faculty_name").Equals(ComboName.Text))
foreach (var row in facultyinfo)
{
//Display selected row elements...
}
```

FIGURE 4.5 An example code for the operator AsEnumerable.

The key point for this query structure is the operator AsEnumerable(). Since different database systems use different collections and query operators, those must be converted to the type of IEnumerable<T> in order to use the data operations in LINQ using a Standard Query Operator that can perform complex data queries on an IEnumerable<T> sequence. Compiling an error would be encountered without this operator.

### Join(Join Purpose)

A join of two data sources is the association of objects in one data source with objects that share a common attribute in another data source. Joining is an important operation in queries whose relationships to each other cannot be followed directly. In object-oriented programming, this could mean a correlation between objects that is not modeled, such as the backwards direction of a
