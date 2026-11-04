The following code shows invoking the Divide() method. The items of the tuple can be accessed with the properties Item1 and Item2;

```
```csharp
var result = Divide(5, 2);
Console.WriteLine("result of division: {0}, reminder: {1}",
    result.Item1, result.Item2);
```
```

In case you have more than eight items that should be included in a tuple, you can use the Tuple class definition with eight parameters. The last template parameter is named TRest to indicate that you must pass a tuple itself. That way you can create tuples with any number of parameters.

To demonstrate this functionality:

```
```csharp
public class Tuple<T1, T2, T3, T4, T5, T6, T7, TRest>
```
```

Here, the last template parameter is a tuple type itself, so you can create a tuple with any number of items:

```
```csharp
var tuple = Tuple.Create<string, string, string, int, int, int, double,
    Tuple<int, int>>(
    "Stephanie", "Alina", "Nagel", 2009, 6, 2, 1.37,
    Tuple.Create<int, int>(52, 3490));
```
```

# THE DYNAMIC TYPE

The dynamic type allows you to write code that will bypass compile time type checking. The compiler will assume that whatever operation is defined for an object of type dynamic is valid. If that operation isn't valid, the error won't be detected until runtime. This is shown in the following example:

```
```csharp
class Program
{
    static void Main(string[] args)
    {
        var staticPerson = new Person();
        dynamic dynamicPerson = new Person();
        staticPerson.GetFullName("John", "Smith");
        dynamicPerson.GetFullName("John", "Smith");
    }
}
class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string GetFullName()
    {
        return string.Concat(FirstName, " ", LastName);
    }
}
```
```

This example will not compile because of the call to staticPerson.GetFullName(). There isn't a method on the Person object that takes two parameters, so the compiler raises the error. If that line of code were to be commented out, the example would compile. If executed, a runtime error