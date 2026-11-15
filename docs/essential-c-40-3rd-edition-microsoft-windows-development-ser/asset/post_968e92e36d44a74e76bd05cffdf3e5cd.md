
Listing 5.20 assigns the field from within the Employee constructor rather than the property (_id = id). Assigning via the property causes a compile error, as it does in Program.Main().

## Access Modifiers on Getters and Setters

As previously mentioned, it is a good practice not to access fields from outside their properties because doing so circumvents any validation or additional logic that may be inserted. Unfortunately, C# 1.0 did not allow different levels of encapsulation between the getter and setter portions of a property. It was not possible, therefore, to create a public getter and a private setter so that external classes would have read-only access to the property while code within the class could write to the property.

In C# 2.0, support was added for placing an access modifier on either the get or the set portion of the property implementation (not on both), thereby overriding the access modifier specified on the property declaration. Listing 5.21 demonstrates how to do this.

### LISTING 5.21: Placing Access Modifiers on the Setter

```
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Initialize(42);

        // ERROR: The property or indexer 'Employee.Id'
        // cannot be used in this context because the set
        // accessor is inaccessible
        employee1.Id = "498";
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
}
// Id property declaration
public string Id
{
    get
    {
        return _id;
    }
    // Providing an access modifier is in C# 2.0
    // and higher only
    private set
    {
        _id = value;
    }
}
private string _id;
}
```

By using private on the setter, the property appears as read-only to classes other than Employee. From within Employee, the property appears as read/write, so you can assign the property within the constructor. When specifying an access modifier on the getter or setter, take care that the access modifier is more restrictive than the access modifier on the property as a whole. It is a compile error, for example, to declare the property as private and the setter as public.

## Properties as Virtual Fields

As you have seen, properties behave like virtual fields. In some instances, you do not need a backing field at all. Instead, the property getter returns a calculated value while the setter parses the value and persists it to some other member fields (if it even exists). Consider, for example, the Name property implementation shown in Listing 5.22. Output 5.7 shows the results.

### LISTING 5.22: Defining Properties

```
class Program
{
    static void Main()
    {
        Employee employee1 = new Employee();
        employee1.Name = "Inigo Montoya";
        System.Console.WriteLine(employee1.Name);
    }
}
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
        get
        {
            return _LastName;
        }
        set
        {
            _LastName = value;
        }
    }
    private string _LastName;
    // ...

// Name property
public string Name
{
    get
    {
        return FirstName + " " + LastName;
    }
    set
    {
        // Split the assigned value into
// first and Last names.
string[] names;
names = value.Split(new char[] { ' ' });
if(names.Length == 2)
{
    FirstName = names[0];
    LastName = names[1];
}
else
{
    // Throw an exception if the full
    // name was not assigned.
    throw new System.ArgumentException(
        string.Format(
            "Assigned value '{0}' is invalid", value));
}
}
// ...
}
```

### Output 5.7:

```
Inigo Montoya
```

The getter for the Name property concatenates the values returned from the FirstName and LastName properties. In fact, the name value assigned is not actually stored. When the Name property is assigned, the value on the right side is parsed into its first and last name parts.

## Properties and Method Calls Not Allowed as ref or out Parameter Values

C# allows properties to be used identically to fields, except when they are passed as ref or out parameter values. ref and out parameter values are internally implemented by passing the memory address to the target method. However, because properties can be virtual fields that have no backing field, or can be read/write-only, it is not possible to pass the address for the underlying storage. As a result, you cannot pass properties as ref or out parameter values. The same is true for method calls. Instead, when code needs to pass a property or method call as a ref or out parameter value, the code must first copy the value into a variable and then pass the variable. Once the method call has completed, the code must assign the variable back into the property.

## ADVANCED TOPIC

## Property Internals

Listing 5.23 shows that getters and setters are exposed as get_FirstName() and set_FirstName() in the CIL.

### LISTING 5.23: CIL Code Resulting from Properties

```
.method public hidebysig specialname instance string
get_FirstName() cil managed
{
    // Code size       12 (0xc)
    .maxstack  1
    .locals init ([0] string CS$1$0000)
    IL_0000:  nop
    IL_0001:  ldarg.0
    IL_0002:  ldfld      string Program::FirstName
    IL_0007:  stloc.0
    IL_0008:  br.s       IL_000a
    IL_000a:  ldloc.0
    IL_000b:  ret
} // end of method Program::get_FirstName

.method public hidebysig specialname instance void
set_FirstName(string value) cil managed
{
    // Code size       9 (0x9)
    .maxstack  8
    IL_0000:  nop
    IL_0001:  ldarg.0
    IL_0002:  ldarg.1
    IL_0003:  stfld      string Program::FirstName
    IL_0008:  ret
} // end of method Program::set_FirstName
```

Just as important to their appearance as regular methods is the fact that properties are an explicit construct within the CIL, too. As Listing 5.24 shows, the getters and setters are called by CIL properties, which are an explicit construct within the CIL code. Because of this, languages and compilers are not restricted to always interpreting properties based on a naming convention. Instead, CIL properties provide a means for compilers and code editors to provide special syntax.

### LISTING 5.24: Properties Are an Explicit Construct in CIL

```
.property instance string FirstName()
{
    .get instance string Program::get_FirstName()
    .set instance void Program::set_FirstName(string)
} // end of property Program::FirstName
```

Notice in Listing 5.23 that the getters and setters that are part of the property include the specialname metadata. This modifier is what IDEs, such as Visual Studio, use as a flag to hide the members from IntelliSense.

An automatically implemented property is virtually identical to one for which you define the backing field explicitly. In place of the manually defined backing field the C# compiler generates a field with the name <PropertyName>k__BackingField in IL. This generated field includes an attribute (see Chapter 17) called System.Runtime.CompilerServices.CompilerGeneratedAttribute. Both the getters and the setters are decorated with the same attribute because they too are generated—with the same implementation as in Listings 5.23 and 5.24.

## Constructors

Now that you have added fields to a class and can store data, you need to consider the validity of that data. As you saw in Listing 5.3, it is possible to instantiate an object using the new operator. The result, however, is the ability to create an employee with invalid data. Immediately following the assignment of employee, you have an Employee object whose name and salary are not initialized. In this particular listing, you assigned the uninitialized fields immediately following the instantiation of an employee, but if you failed to do the initialization, you would not receive a warning from the compiler. As a result, you could end up with an Employee object with an invalid name.
