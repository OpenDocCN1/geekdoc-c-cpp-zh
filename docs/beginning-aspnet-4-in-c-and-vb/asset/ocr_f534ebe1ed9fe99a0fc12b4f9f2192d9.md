The following code shows how invoking the Divide() method. The items of the tuple can be accessed with the properties Item1 and Item2:

```
var result = Divide(5, 2);
Console.WriteLine("result of division: {0}, remainder: {1}",
    result.Item1, result.Item2);
```

In case you have more than eight items that should be included in a tuple, you can use the Tuple class definition with eight parameters. The last template parameter is named TRest to indicate that you must pass a tuple itself. That way you can create tuples with any number of parameters.

To demonstrate this functionality:

```
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest>
```

Here, the last template parameter is a tuple type itself, so you can create a tuple with any number of items:

```
var tuple = Tuple.Create<string, string, string, int, int, int, double,
    Tuple<int, int>>(
    "Stephanie", "Alina", "Nagel", 2009, 6, 2, 1.37,
    Tuple.Create<int, int>(52, 3490));
```

# STRUCTURAL COMPARISON

Both arrays and tuples implement the interfaces IStructuralEquatable and IStructuralComparable. These interfaces are new with .NET 4 and not only compare references but the content as well. This interface is implemented explicitly, so it is necessary to cast the arrays and tuples to this interface on use. IStructuralEquatable is used to compare whether two tuples or arrays have the same content; IStructuralComparable is used to sort tuples or arrays.

With the sample demonstrating IStructuralEquatable, the Person class implementing the interface IEquatable is used. IEquatable defines a strongly typed Equals() method where the values of the FirstName and LastName properties are compared:

```
public class Person : IEquatable<Person>
{
    public int Id { get; private set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }

    public override string ToString()
    {
        return String.Format("{0}, {1} {2}", Id, FirstName, LastName);
    }

    public override bool Equals(object obj)
    {
        if (obj == null) throw new ArgumentNullException("obj");
        return Equals(obj as Person);
    }

    public override int GetHashCode()
    {
        return Id.GetHashCode();
    }

    public bool Equals(Person other)
    {
        if (other == null) throw new ArgumentNullException("other");

        return this.Id == other.Id && this.FirstName == other.FirstName &&
```