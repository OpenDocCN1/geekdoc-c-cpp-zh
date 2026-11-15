
```
return employee;
}
```

```csharp
class Program
{
    static void Main()
    {
        Employee employee1;

        Employee employee2 = new Employee();
        employee2.SetName("Inigo", "Montoya");
        employee2.Save();

        // Modify employee2 after saving.
        IncreaseSalary(employee2);

        // Load employee1 from the saved version of employee2
        employee1 = DataStore.Load("Inigo", "Montoya");

        Console.WriteLine(
            "{0}: {1}",
            employee1.GetName(),
            employee1.Salary);

        // ...
    }
    // ...
}
```

Output 5.4 shows the results.

### OUTPUT 5.4:

```
Name changed to 'Inigo Montoya'
Inigo Montoya
```

The reverse of the save process appears in Listing 5.14, which uses a StreamReader rather than a StreamWriter. Again, Close() needs to be called on both FileStream and StreamReader once the data has been read.

Output 5.4 does not show any salary after “Inigo Montoya.” because Salary was not set to “Enough to survive on” by a call to IncreaseSalary() until after the call to Save().

Notice in Main() that we can call Save() from an instance of an employee, but to load a new employee we call DataStorage.Load(). To load an employee, we generally don't already have an employee instance to load into, so an instance method on Employee would be less than ideal. An alternative to calling Load on DataStorage would be to add a static Load() method (see the section Static, later in this chapter) to Employee so that it would be possible to call Employee.Load() (using the Employee class, not an instance of Employee).

Observe the inclusion of the using System.IO directive at the top of the listing. This makes each IO class accessible without prefixing it with the full namespace.

## Access Modifiers

When declaring a field earlier in the chapter, you prefixed the field declaration with the keyword public. public is an access modifier that identifies the level of encapsulation associated with the member it decorates. Five access modifiers are available: public, private, protected, internal, and protected internal. This section considers the first two.

### BEGINNER TOPIC

## Encapsulation Part 2: Information Hiding

Besides wrapping data and methods together into a single unit, encapsulation is also about hiding the internal details of an object's data and behavior. To some degree, methods do this: from outside a method, all that is visible to a caller is the method declaration. None of the internal implementation is visible. Object-oriented programming enables this further, however, by providing facilities for controlling the extent to which members are visible from outside the class. Members that are not visible outside the class are private members.

In object-oriented programming, encapsulation is the term for not only grouping data and behavior, but also hiding data within a class (the capsule) so that minimum access about the inner workings of a class is exposed outside the class. This reduces the chances that callers will modify the data inappropriately.

The purpose of an access modifier is to provide encapsulation. By using `public`, you explicitly indicated that it is acceptable that the modified fields are accessible from outside the `Employee` class—in other words, that they are accessible from the `Program` class, for example.

Consider an `Employee` class that includes a `Password` field, however. It should be possible to call an `Employee` object and verify the password using a `Logon()` method. It should not be possible, however, to access the `Password` field on an `Employee` object from outside the class.

To define a `Password` field as hidden and inaccessible from outside the containing class, you use the keyword `private` for the access modifier, in place of `public` (see Listing 5.15). As a result, the `Password` field is not intended for access from inside the `Program` class, for example.

### LISTING 5.15: Using the private Access Modifier

```csharp
class Employee
{
    public string FirstName;
    public string LastName;
    public string Salary;
    private string Password;
    private bool IsAuthenticated;
}
```

```csharp
public bool Logon(string password)
{
    if (Password == password)
    {
        IsAuthenticated = true;
    }
    return IsAuthenticated;
}

public bool GetIsAuthenticated()
{
    return IsAuthenticated;
}
```

```csharp
class Program
{
    static void Main()
    {
        Employee employee = new Employee();

        employee.FirstName = "Inigo";
        employee.LastName = "Montoya";

        // ...

        // Password is private, so it cannot be
        // accessed from outside the class.
        // Console.WriteLine(
        // ("Password = {0}", employee.Password);
        // ...
    }
}
```

Although not shown in Listing 5.15, it is possible to decorate a method with an access modifier of private as well.

Note that if no access modifier is placed on a class member, the declaration will default to private. In other words, members are private by default and programmers need to specify explicitly that a member is to be public.

## Properties

The preceding section, Access Modifiers, demonstrated how you can use the private keyword to encapsulate a password, preventing access from outside the class. This type of encapsulation is often too thorough, however. For example, sometimes you might need to define fields that external classes can only read but whose values you can change internally. Alternatively, perhaps you want to allow access to write some data in a class but you need to be able to validate changes made to the data. Still one more example is the need to construct the data on the fly.

Traditionally, languages enabled the features found in these examples by marking fields as private and then providing getter and setter methods for accessing and modifying the data. The code in Listing 5.16 changes both FirstName and LastName to private fields. Public getter and setter methods for each field allow their values to be accessed and changed.

### LISTING 5.16: Declaring Getter and Setter Methods

```csharp
class Employee
{
    private string FirstName;
    // FirstName getter
    public string GetFirstName()
    {
        return FirstName;
    }
    // FirstName setter
    public void SetFirstName(string newFirstName)
    {
        if (newFirstName != null && newFirstName != "")
        {
            FirstName = newFirstName;
        }
    }

    private string LastName;
    // LastName getter
    public string GetLastName()
    {
        return LastName;
    }
    // LastName setter
    public void SetLastName(string newLastName)
    {
        if (newLastName != null && newLastName != "")
        {
            LastName = newLastName;
        }
    }
    // ...
}
```

Unfortunately, this change affects the programmability of the Employee class. No longer can you use the assignment operator to set data within the class, nor can you access data without calling a method.

### Declaring a Property

Considering the frequency of this type of pattern, the C# designers decided to provide explicit syntax for it. This syntax is called a **property** (see Listing 5.17 and Output 5.5).

### LISTING 5.17: Defining Properties

```csharp
class Program
{
    static void Main()
    {
        Employee employee = new Employee();

        // Call the FirstName property's setter.
        employee.FirstName = "Inigo";

        // Call the FirstName property's getter.
        System.Console.WriteLine(employee.FirstName);
    }
}
```

```csharp
class Employee
{
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
}
```
