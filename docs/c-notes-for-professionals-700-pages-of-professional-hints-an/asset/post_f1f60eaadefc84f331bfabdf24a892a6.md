
Less efficient but more general is as follows:

```
Type t = null;
foreach (Assembly ass in AppDomain.CurrentDomain.GetAssemblies())
{
    if (ass.FullName.StartsWith("System."))
        continue;
    t = ass.GetType(typeName);
    if (t != null)
        break;
}
```

Notice the check to exclude scanning System namespace assemblies to speed up the search. If your type may actually be a CLR type, you will have to delete these two lines.

If you happen to have the fully assembly-qualified type name including the assembly you can simply get it with

```
Type.GetType(fullyQualifiedName);
```

### Section 63.12: Determining generic arguments of instances of generic types

If you have an instance of a generic type but for some reason don't know the specific type, you might want to determine the generic arguments that were used to create this instance.

Let's say someone created an instance of List<T> like that and passes it to a method:

```
var myList = new List<int>();
ShowGenericArguments(myList);
```

where ShowGenericArguments has this signature:

```
public void ShowGenericArguments(object o)
```

so at compile time you don't have any idea what generic arguments have been used to create o. Reflection provides a lot of methods to inspect generic types. At first, we can determine if the type of o is a generic type at all:

```
public void ShowGenericArguments(object o)
{
    if (o == null) return;

    Type t = o.GetType();
    if (!t.IsGenericType) return;
    ...
```

Type.IsGenericType returns true if the type is a generic type and false if not.

But this is not all we want to know. List<> itself is a generic type, too. But we only want to examine instances of specific constructed generic types. A constructed generic type is for example a List<int> that has a specific type argument for all its generic parameters.

The Type class provides two more properties, IsConstructedGenericType and IsGenericTypeDefinition, to distinguish these constructed generic types from generic type definitions:

```
typeof(List<>).IsGenericType // true
typeof(List<>).IsGenericTypeDefinition // true
```

```
typeof(List<>).IsConstructedGenericType// false

typeof(List<int>).IsGenericType // true
typeof(List<int>).IsGenericTypeDefinition // false
typeof(List<int>).IsConstructedGenericType// true
```

To enumerate the generic arguments of an instance, we can use the `GetGenericArguments()` method that returns an Type array containing the generic type arguments:

```
public void ShowGenericArguments(object o)
{
    if (o == null) return;
    Type t = o.GetType();
    if (!t.IsConstructedGenericType) return;

    foreach(Type genericTypeArgument in t.GetGenericArguments())
        Console.WriteLine(genericTypeArgument.Name);
}
```

So the call from above (ShowGenericArguments(myList)) results in this output:

```
Int32
```

### Section 63.13: Looping through all the properties of a class

```
Type type = obj.GetType();
//To restrict return properties. If all properties are required don't provide flag.
BindingFlags flags = BindingFlags.Public | BindingFlags.Instance;
PropertyInfo[] properties = type.GetProperties(flags);

foreach (PropertyInfo property in properties)
{
    Console.WriteLine("Name: " + property.Name + ", Value: " + property.GetValue(obj, null));
}
```

## Chapter 64: IQueryable interface

### Section 64.1: Translating a LINQ query to a SQL query

The IQueryable and IQueryable<T> interfaces allows developers to translate a LINQ query (a 'language-integrated' query) to a specific datasource, for example a relational database. Take this LINQ query written in C#:

```
var query = from book in books
    where book.Author == "Stephen King"
    select book;
```

If the variable books is of a type that implements IQueryable<Book> then the query above gets passed to the provider (set on the IQueryable.Provider property) in the form of an expression tree, a data structure that reflects the structure of the code.

The provider can inspect the expression tree at runtime to determine:
- that there is a predicate for the Author property of the Book class;
- that the comparison method used is 'equals' (==);
- that the value it should equal is "Stephen King".

With this information the provider can translate the C# query to a SQL query at runtime and pass that query to a relational database to fetch only those books that match the predicate:

```
SELECT *
FROM Books
WHERE Author = 'Stephen King'
```

The provider gets called when the query variable is iterated over (IQueryable implements IEnumerable).

(The provider used in this example would require some extra metadata to know which table to query and to know how to match properties of the C# class to columns of the table, but such metadata is outside of the scope of the IQueryable interface.)

## Chapter 65: Linq to Objects

LINQ to Objects refers to the use of LINQ queries with any IEnumerable collection.

### Section 65.1: Using LINQ to Objects in C#

### A simple SELECT query in Linq

```
static void Main(string[] args)
{
    string[] cars = { "VW Golf",
                      "Opel Astra",
                      "Audi A4",
                      "Ford Focus",
                      "Seat Leon",
                      "VW Passat",
                      "VW Polo",
                      "Mercedes C-Class" };

    var list = from car in cars
               select car;

    StringBuilder sb = new StringBuilder();

    foreach (string entry in list)
    {
        sb.Append(entry + "\n");
    }

    Console.WriteLine(sb.ToString());
    Console.ReadLine();
}
```

In the example above, an array of strings (cars) is used as a collection of objects to be queried using LINQ. In a LINQ query, the from clause comes first in order to introduce the data source (cars) and the range variable (car). When the query is executed, the range variable will serve as a reference to each successive element in cars. Because the compiler can infer the type of car, you do not have to specify it explicitly

When the above code is compiled and executed, it produces the following result:

![](img/5da9b5c72747b887ec63f57c832400bf_366_0.png)

### SELECT with a WHERE Clause

```
var list = from car in cars
           where car.Contains("VW")
           select car;
```

The WHERE clause is used to query the string array (cars) to find and return a subset of array which satisfies the WHERE clause.

When the above code is compiled and executed, it produces the following result:

![](img/5da9b5c72747b887ec63f57c832400bf_367_0.png)

### Generating an Ordered List

```
var list = from car in cars
           orderby car ascending
           select car;
```

Sometimes it is useful to sort the returned data. The orderby clause will cause the elements to be sorted according to the default comparer for the type being sorted.

When the above code is compiled and executed, it produces the following result:

![](img/5da9b5c72747b887ec63f57c832400bf_367_1.png)

### Working with a custom type

In this example, a typed list is created, populated, and then queried

```
public class Car
{
    public String Name { get; private set; }
    public int UnitsSold { get; private set; }

    public Car(string name, int unitsSold)
    {
        Name = name;
        UnitsSold = unitsSold;
    }
}

class Program
{
    static void Main(string[] args)
    {
        var car1 = new Car("VW Golf", 270952);
        var car2 = new Car("Opel Astra", 56079);
        var car3 = new Car("Audi A4", 52493);
        var car4 = new Car("Ford Focus", 51677);
        var car5 = new Car("Seat Leon", 42125);
        var car6 = new Car("VW Passat", 97586);
        var car7 = new Car("VW Polo", 69867);
        var car8 = new Car("Mercedes C-Class", 67549);

        var cars = new List<Car> {
            car1, car2, car3, car4, car5, car6, car7, car8 };
        var list = from car in cars
            select car.Name;

        foreach (var entry in list)
        {
            Console.WriteLine(entry);
        }
        Console.ReadLine();
    }
}
```

When the above code is compiled and executed, it produces the following result:

![](img/5da9b5c72747b887ec63f57c832400bf_368_0.png)

Until now the examples don't seem amazing as one can just iterate through the array to do basically the same.

However, with the few examples below you can see how to create more complex queries with LINQ to Objects and achieve more with a lot less of code.

In the example below we can select cars that have been sold over 60000 units and sort them over the number of units sold:

```
var list = from car in cars
    where car.UnitsSold > 60000
    orderby car.UnitsSold descending
    select car;

StringBuilder sb = new StringBuilder();

foreach (var entry in list)
{
    sb.AppendLine($"{entry.Name} - {entry.UnitsSold}");
}
Console.WriteLine(sb.ToString());
```

When the above code is compiled and executed, it produces the following result:
