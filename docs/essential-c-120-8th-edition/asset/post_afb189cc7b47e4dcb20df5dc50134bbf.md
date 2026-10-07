
# Chapter 6: Classes

- DO declare all instance fields as private (and expose them via a property).
- DO name properties with PascalCase.
- DO favor automatically implemented properties over fields.
- DO favor automatically implemented properties over using fully expanded ones if there is no additional implementation logic.

## Using Properties with Validation

Notice in Listing 6.20 that the Initialize() method of Employee uses the property rather than the field for assignment as well. Although this is not required, the result is that any validation within the property setter will be invoked inside and outside the class. Consider, for example, what would happen if you changed the LastName property so that it checked for null or an empty string before assigning it to _LastName. (Recall checking for null is necessary even though the data is a non-nullable string, the caller may have nullable reference types disabled, or the method may be invoked from C# 7.0 or earlier—before nullable reference types existed.)

## Listing 6.20: Providing Property Validation

```c
public class Employee
{
    // ...
    public void Initialize(
        string firstName, string lastName)
    {
        // Use property inside the Employee
        // class as well
        FirstName = firstName;
        LastName = lastName;
    }
}

// LastName property
public string LastName
{
    get => _LastName;
    set
    {
        // ...
        // Validate LastName assignment
        ArgumentException.ThrowIfNullOrEmpty(value = value?.Trim()!);
        // ...
        _LastName = value;
    }
    private string _LastName;
}
```

With this new implementation, the code throws an exception if LastName is assigned an invalid value, either from another member of the same class or via a direct assignment to LastName from inside Program.Main(). The ability to intercept an assignment and validate the parameters by providing a field-like API is one of the advantages of properties.

It is a good practice to access the backing field from inside the property implementation. In other words, you should always use the property rather than calling the field directly. In many cases, this principle holds even from code within the same class as the property. If you follow this practice, you can add code such as validation, the entire class immediately takes advantage of it.^5

Although rare, it is possible to assign value inside the setter, as Listing 6.20 does. In this case, the call to value.Trim() removes any whitespace surrounding the new last name value.

![](img/ffe0f34eac7523830420733690014d17_359_0.png)

## Guidelines

- AVOID accessing the backing field of a property outside the property, even from within the containing class.

> ^5. As described later in the chapter, one exception to this occurs when the field is marked as readonly, because then the value can be set only in the constructor. In C# 6.0, you can directly assign the value of a read-only property, completely eliminating the need for the read-only field.

## Read-Only and Write-Only Properties

By removing either the getter or the setter portion of a property, you can change a property’s accessibility. Properties with only a setter are write-only, which is relatively rare. Similarly, providing only a getter will cause the property to be read-only; any attempts to assign a value will cause a compiler error. To make Id read-only, for example, you would use the code shown in Listing 6.21.

## LISTING 6.21: Defining a Read-Only Property Prior to C# 6.0

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee1 = new();
        employee1.Initialize(42);

        // ERROR: Property or indexer 'Employee.Id'
        // cannot be assigned to; it is read-only
        employee1.Id = "498";
    }
}
```

```csharp
public class Employee
{
    public void Initialize(int id)
    {
        // Use field because Id property has no setter;
        // it is read-only
        _Id = id.ToString();
    }

    // ...
    // Id property declaration
    public string Id
    {
        get => _Id;
        // No setter provided
    }
    private string _Id;
}
```

Listing 6.21 assigns the field from within the Employee Initialize() method rather than the property (_Id = id). Assigning via the property causes a compile error, as it does in Program.Main().

There is also support for read-only, automatically implemented properties,^6 as follows:

```csharp
public bool[] Cells { get; } = new bool[9];
```

One important note about a read-only automatically implemented property is that, like read-only fields, the compiler requires that such a property be initialized via an auto-property initializer (or in the constructor). In the preceding snippet we use an initializer, but the assignment of Cells from within the constructor is also permitted, as we shall shortly see.

Given the guideline that fields should not be accessed from outside their wrapping property, the programmer should instead use a read-only, automatically implemented property. The only exception might be when the data type of the read-only modified field does not match the data type of the property—for example, if the field was of int and the read-only property was of type double.

> Guidelines
> **DO create read-only properties if the property value should not be changed.**
> **DO create read-only automatically implemented properties, rather than backing fields.**

## Calculated Properties

In some instances, you do not need a backing field at all. Instead, the getter returns a calculated value, while the setter parses the value and persists it to some other fields. Consider, for example, the Name property shown in Listing 6.22.

## LISTING 6.22: Defining Calculated Properties

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee1 = new();
        employee1.Name = "Inigo Montoya";
        Console.WriteLine(employee1.Name);
    }
}

public class Employee
{
    // ...
    public string Name
    {
        get => $"{FirstName} {LastName}";
        set 
        {
            // Split the assigned value into first and last names
            string[] names;
            names = value.Split(new char[] { ' ' });
            if (names.Length == 2)
            {
                FirstName = names[0];
                LastName = names[1];
            }
            else
            {
                // Throw an exception if the full name was not assigned
                throw new ArgumentException("Assigned value '{value}' is invalid", nameof(value));
            }
        }
    }

    // FirstName property
    public string FirstName
    {
        get => _FirstName;
        set => _FirstName = value;
    }
    private string _FirstName;

    // LastName property
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;
}
```

## OUTPUT 6.7

| Inigo Montoya |

## Access Modifiers on Getters and Setters

As previously mentioned, it is a good practice not to access fields from outside properties because doing so circumvents any validation or additional logic that may be inserted.

An access modifier can appear on either the get or the set portion of the property implementation (not on both), thereby overriding the access modifier specified on the property declaration. Listing 6.23 demonstrates how to do this.

## Listing 6.23: Placing Access Modifiers on the Setter

```csharp
public class Program
{
    public static void Main()
    {
        Employee employee1 = new();
        employee1.Initialize(42);
        // ERROR: The property or indexer 'Employee.Id'
        // cannot be used in this context because the set
        // accessor is inaccessible
        employee1.Id = "496";
    }
}
```

```csharp
public class Employee
{
    public void Initialize(int id)
    {
        // Set Id property
        Id = id.ToString();
    }

    //...
    // Id property declaration
    public string Id
    {
        get => _Id;
        private set => _Id = value;
    }
    private string _Id;
}
```

+   6. Introduced in C# 2.0. C# 1.0 did not allow different levels of encapsulation and setter portions of a property. It was not possible, therefore, to create a public getter and a private setter so that external classes would have read-only access to the property while code within the class could write to it.
