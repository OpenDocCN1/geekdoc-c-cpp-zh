
```csharp
{
    return "Derived";
}
}
public static class Program
{
    public static void Main()
    {
        Derived derived = new Derived();
        Base @base = derived;

        // Use the instance method "GetName"
        Console.WriteLine(derived.GetName()); // Prints "Derived"
        Console.WriteLine(@base.GetName()); // Prints "Derived"

        // Use the static extension method "GetNameByExtension"
        Console.WriteLine(derived.GetNameByExtension()); // Prints "Derived"
        Console.WriteLine(@base.GetNameByExtension()); // Prints "Base"
    }
}
```

Live Demo on .NET Fiddle

Also the dispatch based on static type does not allow an extension method to be called on a dynamic object:

```csharp
public class Person
{
    public string Name { get; set; }
}

public static class ExtensionPerson
{
    public static string GetPersonName(this Person person)
    {
        return person.Name;
    }
}

dynamic person = new Person { Name = "Jon" };
var name = person.GetPersonName(); // RuntimeBinderException is thrown
```

## Section 48.9: Extension methods on Interfaces

One useful feature of extension methods is that you can create common methods for an interface. Normally an interface cannot have shared implementations, but with extension methods they can.

```csharp
public interface IVehicle
{
    int MilesDriven { get; set; }
}

public static class Extensions
{
    public static int FeetDriven(this IVehicle vehicle)
    {
        return vehicle.MilesDriven * 5280;
    }
}
```

In this example, the method FeetDriven can be used on any IVehicle. The logic in this method would apply to all IVehicles, so it can be done this way so that there doesn't have to be a FeetDriven in the IVehicle definition which would be implemented the same way for all children.

## Section 48.10: Extension methods in combination with interfaces

It is very convenient to use extension methods with interfaces as implementation can be stored outside of class and all it takes to add some functionality to class is to decorate class with interface.

```csharp
public interface IInterface
{
    string Do()
}

public static class ExtensionMethods{
    public static string DoWith(this IInterface obj){
        //does something with IInterface instance
    }
}

public class Classy : IInterface
{
    // this is a wrapper method; you could also call DoWith() on a Classy instance directly,
    // provided you import the namespace containing the extension method
    public string Do(){
        return this.DoWith();
    }
}
```

use like:

```csharp
var classy = new Classy();
classy.Do(); // will call the extension
classy.DoWith(); // Classy implements IInterface so it can also be called this way
```

## Section 48.11: Extension methods aren't supported by dynamic code

```csharp
static class Program
{
    static void Main()
    {
        dynamic dynamicObject = new ExpandoObject();

        string awesomeString = "Awesome";

        // Prints True
        Console.WriteLine(awesomeString.IsThisAwesome());

        dynamicObject.StringValue = awesomeString;

        // Prints True
        Console.WriteLine(StringExtensions.IsThisAwesome(dynamicObject.StringValue));

        // No compile time error or warning, but on runtime throws RuntimeBinderException
        Console.WriteLine(dynamicObject.StringValue.IsThisAwesome());
    }
}
```

```csharp
static class StringExtensions
{
    public static bool IsThisAwesome(this string value)
    {
        return value.Equals("Awesome");
    }
}
```

The reason [calling extension methods from dynamic code] doesn't work is because in regular, non-dynamic code extension methods work by doing a full search of all the classes known to the compiler for a static class that has an extension method that matches. The search goes in order based on the namespace nesting and available using directives in each namespace.

That means that in order to get a dynamic extension method invocation resolved correctly, somehow the DLR has to know at runtime what all the namespace nestings and using directives were in your source code. We do not have a mechanism handy for encoding all that information into the call site. We considered inventing such a mechanism, but decided that it was too high cost and produced too much schedule risk to be worth it.

Source

## Section 48.12: Extensions and interfaces together enable DRY code and mixin-like functionality

Extension methods enable you to simplify your interface definitions by only including core required functionality in the interface itself and allowing you to define convenience methods and overloads as extension methods.

Interfaces with fewer methods are easier to implement in new classes. Keeping overloads as extensions rather than including them in the interface directly saves you from copying boilerplate code into every implementation, helping you keep your code DRY. This in fact is similar to the mixin pattern which C# does not support.

System.Linq.Enumerable's extensions to IEnumerable<T> is a great example of this. IEnumerable<T> only requires the implementing class to implement two methods: generic and non-generic GetEnumerator(). But System.Linq.Enumerable provides countless useful utilities as extensions enabling concise and clear consumption of IEnumerable<T>.

The following is a very simple interface with convenience overloads provided as extensions.

```csharp
public interface ITimeFormatter
{
    string Format(TimeSpan span);
}

public static class TimeFormatter
{
    // Provide an overload to *all* implementers of ITimeFormatter.
    public static string Format(
        this ITimeFormatter formatter,
        int millisecondsSpan)
        => formatter.Format(TimeSpan.FromMilliseconds(millisecondsSpan));
}

// Implementations only need to provide one method. Very easy to
// write additional implementations.
```

```csharp
public class SecondsTimeFormatter : ITimeFormatter
{
    public string Format(TimeSpan span)
    {
        return $"{(int)span.TotalSeconds}s";
    }
}
class Program
{
    static void Main(string[] args)
    {
        var formatter = new SecondsTimeFormatter();
        // Callers get two method overloads!
        Console.WriteLine($"4500ms is roughly {formatter.Format(4500)}");
        var span = TimeSpan.FromSeconds(5);
        Console.WriteLine($"{span} is formatted as {formatter.Format(span)}");
    }
}
```

## Section 48.13: IList<T> Extension Method Example: Comparing 2 Lists

You can use the following extension method for comparing the contents of two IList<T> instances of the same type.

By default the items are compared based on their order within the list and the items themselves, passing false to the isOrdered parameter will compare only the items themselves regardless of their order.

For this method to work, the generic type (T) must override both Equals and GetHashCode methods.

### Usage:

```csharp
List<string> list1 = new List<string> {"a1", "a2", null, "a3"};
List<string> list2 = new List<string> {"a1", "a2", "a3", null};

list1.Compare(list2);//this gives false
list1.Compare(list2, false);//this gives true. they are equal when the order is disregarded
```

### Method:

```csharp
public static bool Compare<T>(this IList<T> list1, IList<T> list2, bool isOrdered = true)
{
    if (list1 == null && list2 == null)
        return true;
    if (list1 == null || list2 == null || list1.Count != list2.Count)
        return false;

    if (isOrdered)
    {
        for (int i = 0; i < list2.Count; i++)
        {
            var l1 = list1[i];
            var l2 = list2[i];
            if (
                (l1 == null && l2 != null) ||
                (l1 != null && l2 == null) ||
                (!l1.Equals(l2))
            )
            {
                return false;
            }
        }
        return true;
    }
    else
    {
        List<T> list2Copy = new List<T>(list2);
        //Can be done with Dictionary without O(n^2)
        for (int i = 0; i < list1.Count; i++)
        {
            if (!list2Copy.Remove(list1[i]))
                return false;
        }
        return true;
    }
}
```

## Section 48.14: Extension methods as strongly typed wrappers

Extension methods can be used for writing strongly typed wrappers for dictionary-like objects. For example a cache, HttpContext.Items at cetera...

```csharp
public static class CacheExtensions
{
    public static void SetUserInfo(this Cache cache, UserInfo data) =>
        cache["UserInfo"] = data;

    public static UserInfo GetUserInfo(this Cache cache) =>
        cache["UserInfo"] as UserInfo;
}
```

This approach removes the need of using string literals as keys all over the codebase as well as the need of casting to the required type during the read operation. Overall it creates a more secure, strongly typed way of interacting with such loosely typed objects as Dictionaries.

## Section 48.15: Using Extension methods to create beautiful mapper classes

We can create a better mapper classes with extension methods, Suppose if I have some DTO classes like

```csharp
public class UserDTO
{
    public AddressDTO Address { get; set; }
}

public class AddressDTO
{
    public string Name { get; set; }
}
```

and I need to map to corresponding view model classes

```csharp
public class UserViewModel
{
    public AddressViewModel Address { get; set; }
}
```
