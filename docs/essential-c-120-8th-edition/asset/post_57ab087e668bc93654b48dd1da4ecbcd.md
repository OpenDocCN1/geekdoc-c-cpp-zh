
## LISTING 6.41: Using NullWhen and NullIfNotNull Attributes

```c
using System.Diagnostics.CodeAnalysis;
// ...
 static bool TryGetDigitAsText(
    char number, [NotNullWhen(true)]out string text) =
    (text = number switch
    {
        '1' => "one",
        '2' => "two",
        '3' => "three",
        '4' => "four",
        // ...
        '9' => "nine",
        => null
    }) is not null;
```

```c
// nameof(text) on parameters is not supported prior to C# 11/.NET 7.0
[return: NullIfIfNotNull(nameof(text))]
static public string TryGetDigitsAsText(string text)
{
    if (text == null) return null;

    string result = "";
    foreach (char character in text)
    {
        if (TryGetDigitAsText(character, out string digitText))
        {
            if (result != "") result += '-';
            result += digitText.ToLower();
        }
    }
    return result;
}
```

Notice that the call to digitText.ToLower() from TryGetDigitAsText() without a coalescing operator does not issue a warning even though text is declared as nullable. This is possible because the text parameter in TryGetDigitAsText() is decorated with the NullWhen(true) attribute, which informs the compiler that, if the method returns true (the value specified by the NullWhen attribute), then your intent is that digitText will not be null. The NullWhen attribute is a post-condition declaration, informing the caller that output(text) is not null if the method returns true.

Similarly, for GetDigitsAsText(), if the value specified for the text parameter is not null, then the return value will not be null. This is possible because the pre-condition null attribute, NullIfNotNull, uses whether the input value of the text parameter is null to determine whether the return value may potentially be null.

## ADVANCED TOPIC

## Decorating Generic Type Parameters with the Null Modifier

When declaring a generic modifier or type, you will occasionally want to decorate the type parameter with a nullable modifier. The problem is that a nullable type (a `Nullable<T>`) is a different data type than a nullable reference type. As a result, type parameters decorated with nullability will require a constraint that restricts the type parameter to either a value type or a reference type. Without this constraint, you will receive the following error:

```
Error CS8627 A type parameter must be known to be a value type or non-nullable reference type. Consider adding a 'class', 'struct', or type constraint.
```

However, if the logic is identical for both value types and reference types, it can be frustrating to implement two different methods—especially since different constraints do not result in different signatures to allow overloading. Consider the code in 6.42.

Listing 6.42: Potential Null Return With MaybeNull Attribute

```csharp
// ...
[return: MaybeNull]
static public T GetObject<T>(
IEnumerable<T> sequence, Func<T, bool> match)
=>
// ...
```

Imagine the behavior is to return an item from the collection if one satisfies the match predicate. However, if no such item exists, the intent would be to return default(T), which is null for a reference type. Unfortunately, the compiler won't allow T? without a constraint. To avoid the warning while still declaring to callers that the return could be null, we use the post-condition MaybeNull attribute and leave the return type as T (with no nullable modifier).

## Deconstructors

Constructors allow you to take multiple parameters and encapsulate them all into a single object. Until now, we haven't introduced any constructs for implementing the reverse—unwrapping the encapsulated item into its constituent parts. Sure, you could manually assign each property to a variable; however, if there were a significant number of such variables, it would require many separate statements. With tuples, however, this becomes significantly easier. You could, for example, declare a method like the Deconstruct() method shown in Listing 6.43.

LISTING 6.43: Defining and Using a Deconstructor

```csharp
public class Employee
{
    // ...
    public void Deconstruct(
        out int id, out string firstName,
        out string lastName, out string salary)
    {
        (id, firstName, lastName, salary) =
        (Id, FirstName, LastName, Salary);
    }
    // ...
}

public class Program
{
    public static void Main()
    {
        Employee employee;
        employee = new ("Inigo", "Montoya")
        {
            // Leveraging object initializer syntax
            Salary = "Too Little"
        };
        // ...
        employee.Deconstruct(out _, out string firstName,
        out string lastName, out string? salary);

        System.Console.WriteLine(
            "{0} {1}: {2}",
            firstName, lastName, salary);
        );
    }
}
```

Such a method could be invoked directly, as one would expect from Chapter 5, by declaring the out parameters inline. However, you can invoke Deconstruct() method—the deconstructor¹²²—implicitly by assigning the object instance to a tuple directly as shown in Listing 6.44.

## Listing 6.44: Implicitly Invoking Deconstructors

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee;
        employee = new ("Inigo", "Montoya")
        {
            // Leveraging object initializer syntax
            Salary = "Too Little"
        }
        // ...
        (_, string firstName, string lastName, string? salary) = employee;

        System.Console.WriteLine(
            "{0} {1}: {2}",
            firstName, lastName, salary);
        );
    }
}
```

The syntax results in the identical CIL code as highlighted in Listing 6.43—it is just a simpler syntax (and a little less indicative of the Deconstruct() method is invoked). Note that the syntax allows for variables matching the out parameter assignments using tuple syntax. It does not allow for the assignment of a tuple type, either

```csharp
(int, string, string, string) tuple = employee;
```

or with named items as in

```csharp
(int id, string firstName, string lastName, string salary) tuple = employee
```

To declare a deconstructor, the method name must be Deconstruct and have a signature that returns void and exclusively accepts two or more out parameters. And, given such a signature, it is possible to assign an object instance directly to a tuple without the explicit invocation. Note that prior to C# 10, all the assigned values needed to be declared or pre-declared. With C# 10, this restriction was removed.

## Static Members

The HelloWorld example in Chapter 1 briefly touched on the static. This section defines the static keyword more fully. First, let's consider an example. Assume that the employee Id needs to be unique for each employee. One way to accomplish this is to store a counter to track each employee. If the value is stored as an instance field, however every time you instantiate an object, a new NextId field will be created such that every instance of Employee consume memory for that field. The biggest problem is that each time an Employee is instantiated, the NextId value on all of the previously instantiated objects needs to be updated with the next ID. In this case, what you need is a single field that all Employee instances share.

## Language Contrast: C++—Global Variables and Functions

Unlike many of the languages that came before it, C# does not have global variables or global functions. All fields and methods in C# appear within the context of a class. The equivalent of a global field or function within the realm of C# is a static field or function. There is no functional difference between global variables/functions and C# static fields/methods, except that static fields/methods can include access modifiers, such as private, that can limit the access and provide better encapsulation.

## Static Fields

To define data that is available across multiple instances, you use the static keyword, as demonstrated in Listing 6.45.

Listing 6.45: Declaring a Static Field

```csharp
public class Employee
{
    public Employee(string firstName, string lastName)
    {
        FirstName = firstName;
        LastName = lastName;
        Id = NextId;
        NextId++;
    }
    // ...

    public static int NextId;
    public int Id { get; set; }
    public string FirstName { get; set; }
    public string LastName { get; set; }
    public string? Salary { get; set; } = "Not Enough";

    // ...
}
```

12. Introduced in C# 7.0.
