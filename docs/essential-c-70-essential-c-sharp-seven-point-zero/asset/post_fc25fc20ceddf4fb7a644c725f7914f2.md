
The advantage of using the nameof operator is that if the identifier name changes, then refactoring tools will automatically change the argument to nameof as well. If no refactoring tool is used, the code will no longer compile, forcing the developer to change the argument manually.

In the case of a property validator, the parameter is always value and cannot be changed, so the benefits of leveraging the nameof operator are arguably lost. Nonetheless, consider continued use of the nameof operator in all cases of the paramName argument to remain consistent with the guideline: Always use nameof for the paramName argument passed into exceptions like ArgumentNullException and ArgumentException that take such a parameter.

## Read-Only and Write-Only Properties

By removing either the getter or the setter portion of a property, you can change a property's accessibility. Properties with only a setter are write-only, which is a relatively rare occurrence. Similarly, providing only a getter will cause the property to be read-only; any attempts to assign a value will cause a compile error. To make Id read-only, for example, you would code it as shown in Listing 6.21.

### LISTING 6.21: Defining a Read-Only Property Prior to C# 6.0

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Initialize(42);
        // ERROR: Property or indexer 'Employee.Id'
        // cannot be assigned to; it is read-only
        // employee1.Id = "498";
    }
}

class Employee
{
    public void Initialize(int id)
    {
        // Use field because Id property has no setter;
        // it is read-only
        _Id = id.ToString();
    }
}
```

```csharp
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

Starting in C# 6.0, there is also support for read-only, **automatically implemented properties** as follows:

```csharp
public bool[,] Cells { get; } = new bool[2, 3, 3];
```

This is clearly a significant improvement over the pre-C# 6.0 approach, especially given the commonality of read-only properties for something like an array of items or the Id in Listing 6.21.

One important note about a read-only automatically implemented property is that, like read-only fields, the compiler requires that it be initialized via an initializer (or in the constructor). In the preceding snippet we use an initializer, but the assignment of Cells from within the constructor is also permitted, as we shall see shortly.

Given the guideline that fields should not be accessed from outside their wrapping property, those programming in a C# 6.0 world will discover that there is virtually no need to ever use pre-C# 6.0 syntax; instead, the programmer can always use a read-only, automatically implemented property. The only exception might be when the data type of the read-only modified field does not match the data type of the property—for example, if the field was of type int and the read-only property was of type double.

## Guidelines

- DO create read-only properties if the property value should not be changed.
- DO create read-only automatically implemented properties in C# 6.0 (or later) rather than read-only properties with a backing field if the property value should not be changed.

## Properties as Virtual Fields

As you have seen, properties behave like virtual fields. In some instances, you do not need a backing field at all. Instead, the property getter returns a calculated value, while the setter parses the value and persists it to some other member fields (if it even exists). Consider, for example, the Name property implementation shown in Listing 6.22. Output 6.7 shows the results.

### LISTING 6.22: Defining Properties

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();

        employee1.Name = "Inigo Montoya";
        System.Console.WriteLine(employee1.Name);

        // ...
    }
}

class Employee
{
    // ...

    // FirstName property
    public string FirstName
    {
        get
        {
            return _FirstName;
        }
        set
        {
            _FirstName = value;
        }
    }
    private string _FirstName;

    // LastName property
    public string LastName
    {
        get => _LastName;
        set => _LastName = value;
    }
    private string _LastName;
    // ...

    // Name property
    public string Name
    {
        get
        {
            return $"{ FirstName } { LastName }";
        }
        set
        {
            // Split the assigned value into
            // first and last names
            string[] names;
            names = value.Split(new char[]{' '});
            if(names.Length == 2)
            {
                FirstName = names[0];
                LastName = names[1];
            }
            else
            {
                // Throw an exception if the full
                // name was not assigned
                throw new System. ArgumentException (
                    $"Assigned value '{ value }' is invalid", "value");
            }
        }
    }
    public string Initials => $"{ FirstName[0] } { LastName[0] }";
    // ...
}
```

### OUTPUT 6.7

Inigo Montoya

The getter for the Name property concatenates the values returned from the FirstName and LastName properties. In fact, the name value assigned is not actually stored. When the Name property is assigned, the value on the right side is parsed into its first and last name parts.

## Access Modifiers on Getters and Setters

As previously mentioned, it is a good practice not to access fields from outside their properties because doing so circumvents any validation or additional logic that may be inserted. Unfortunately, C# 1.0 did not allow different levels of encapsulation between the getter and setter portions of a property. It was not possible, therefore, to create a public getter and a private setter so that external classes would have read-only access to the property while code within the class could write to the property.

In C# 2.0, support was added for placing an access modifier on either the get or the set portion of the property implementation (not on both), thereby overriding the access modifier specified on the property declaration. Listing 6.23 demonstrates how to do this.

### Listing 6.23: Placing Access Modifiers on the Setter

```csharp
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Initialize(42);
        // ERROR: The property or indexer 'Employee.Id'
        // cannot be used in this context because the set
        // accessor is inaccessible
        employee1.Id = "490";
    }
}

class Employee
{
    public void Initialize(int id)
    {
        // Set Id property
        Id = id.ToString();
    }
    // ...
    // Id property declaration
    public string Id
    {
        get => _Id;
        // Providing an access modifier is possible in C# 2.0
        // and higher only
        private set => _Id = value;
    }
    private string _Id;
}
```

By using private on the setter, the property appears as read-only to classes other than Employee. From within Employee, the property appears as read/write, so you can assign the property within the class itself. When specifying an access modifier on the getter or setter, take care that the access modifier is more restrictive than the access modifier on the property as a whole. It is a compile error, for example, to declare the property as *private* and the setter as *public*.

## Guidelines

- DO apply appropriate accessibility modifiers on implementations of getters and setters on all properties.
- DO NOT provide set-only properties or properties with the setter having broader accessibility than the getter.

## Properties and Method Calls Not Allowed as *ref* or *out* Parameter Values

C# allows properties to be used identically to fields, except when they are passed as *ref* or *out* parameter values. *ref* and *out* parameter values are internally implemented by passing the memory address to the target method. However, because properties can be *virtual* fields that have no backing field or can be *read-only* or *write-only*, it is not possible to pass the address for the underlying storage. As a result, you cannot pass properties as *ref* or *out* parameter values. The same is true for method calls. Instead, when code needs to pass a property or method call as a *ref* or *out* parameter value, the code must first copy the value into a variable and then pass the variable. Once the method call has completed, the code must assign the variable back into the property.

## ADVANCED TOPIC

## Property Internals

Listing 6.24 shows that getters and setters are exposed as `get_FirstName()` and `set_FirstName()` in the Common Intermediate Language (CIL).

### LISTING 6.24: CIL Code Resulting from Properties

```cil
// ...
.field private string _FirstName
.method public hidebysig specialname instance string
    get_FirstName() cil managed
```
