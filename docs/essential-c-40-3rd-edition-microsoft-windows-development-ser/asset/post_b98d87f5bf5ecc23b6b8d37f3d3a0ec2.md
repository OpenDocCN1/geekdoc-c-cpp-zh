
immediately before incrementing it. When another Employee class is created, NextId will be incremented and the new Employee object's Id field will hold a different value.

Just as instance fields (nonstatic fields) can be initialized at declaration time, so can static fields, as demonstrated in Listing 5.35.

### LISTING 5.35: Assigning a Static Field at Declaration

```
class Employee
{
    // ...
    public static int NextId = 42;
    // ...
}
```

Unlike with instance fields, if no initialization for a static field is provided, the static field will automatically be assigned its default value (0, null, false, and so on), and it will be possible to access the static field even if it has never been explicitly assigned.

Nonstatic fields, or instance fields, have a new value for each object to which they belong. In contrast, static fields don't belong to the instance, but rather to the class itself. As a result, you access a static field from outside a class via the class name. Consider the new Program class shown in Listing 5.36 (using the Employee class from Listing 5.34).

### LISTING 5.36: Accessing a Static Field

```
using System;

class Program
{
    static void Main()
    {
        Employee.NextId = 1000000;

        Employee employee1 = new Employee(
            "Inigo", "Montoya");
        Employee employee2 = new Employee(
            "Princess", "Buttercup");

        Console.WriteLine(
            "{0} {1} ({2})",
            employee1.FirstName,
            employee1.LastName,
            employee1.Id);

        Console.WriteLine(
            "{0} {1} ({2})",
            employee2.FirstName,
            employee2.LastName,
            employee2.Id);
        Console.WriteLine("NextId = {0}", Employee.NextId);
    }
}
// ...
```

Output 5.9 shows the results of Listing 5.36.

### Output 5.9:

```
Inigo Montoya (1000000)
Princess Buttercup (1000001)
NextId = 1000002
```

To set and retrieve the initial value of the NextId static field, you use the class name, Employee, not a variable name. The only time you can eliminate the class name is from within code that appears within the class itself. In other words, the Employee(...) constructor did not need to use Employee.NextId because the code appeared within the context of the Employee class itself, and therefore, the context was already understood from the scope. In fact, the context is the scope.

Even though you refer to static fields slightly differently than instance fields, it is not possible to define a static and an instance field with the same name in the same class. The possibility of mistakenly referring to the wrong field is high, and therefore, the C# designers decided to prevent such code. Therefore, overlap in names will introduce conflict within the declaration space.

## BEGINNER TOPIC

### Data Can Be Associated with Both a Class and an Object

Both classes and objects can have associated data, just as can the molds and the widgets created from them.

For example, a mold could have data corresponding to the number of widgets it created, the serial number of the next widget, the current color of the plastic injected into the mold, and the number of widgets it produces per hour. Similarly, a widget has its own serial number, its own color, and perhaps the date and time when the widget was created. Although the color of the widget corresponds to the color of the plastic within the mold at the time the widget was created, it obviously does not contain data corresponding to the color of the plastic currently in the mold, or the serial number of the next widget to be produced.

In designing objects, programmers should take care to declare both fields and methods appropriately as static or instance-based. In general, you should declare methods that don't access any instance data as static methods, and methods that access instance data (where the instance is not passed in as a parameter) as instance methods. Static fields store data corresponding to the class, such as defaults for new instances or the number of instances that have been created. Instance fields store data associated with the object.

## Static Methods

Just like static fields, you access static methods directly off the class name (Console.ReadLine(), for example). Furthermore, it is not necessary to have an instance in order to access the method.

Listing 5.37 provides another example of both declaring and calling a static method.

### LISTING 5.37: Defining a Static Method on DirectoryInfo

```
public static class DirectoryInfoExtension
{
    public static void CopyTo(
        DirectoryInfo sourceDirectory, string target,
        SearchOption option, string searchPattern)
    {
        if (target[target.Length - 1] !=
            Path.DirectorySeparatorChar)
        {
            target += Path.DirectorySeparatorChar;
        }
        if ((Directory.Exists(target))
        {
            Directory.CreateDirectory(target);
        }

        for (int i = 0; i < searchPattern.Length; i++)
        {
            foreach (string file in
            Directory.GetFiles(
            sourceDirectory.FullName, searchPattern))
            {
            File.Copy(file,
            target + Path.GetFileName(file), true);
            }
        }

        //Copy SubDirectories (recursively)
        if (option == SearchOption.AllDirectories)
        {
            foreach (string element in
            Directory.GetDirectories(
            sourceDirectory.FullName))
            {
            Copy(element,
            target + Path.GetFileName(element),
            searchPattern);
            }
        }
    }
}

// ...
DirectoryInfo directory = new DirectoryInfo(".\\Source");
directory.MoveTo(".\\Root");
DirectoryInfoExtension.CopyTo(
directory, ".\\Target",
SearchOption.AllDirectories, "**");
// ...
```

The DirectoryInfoExtension.Copy() method takes a DirectoryInfo object and copies the underlying directory structure to a new location.

Because static methods are not referenced through a particular instance, the this keyword is invalid inside a static method. In addition, it is not possible to access either an instance field or an instance method directly from within a static method without a reference to the particular instance to which the field or method belongs. (Note that Main() is another example of a static method.)

One might have expected this method on the System.IO.Directory class or as an instance method on System.IO.DirectoryInfo. Since neither exists, Listing 5.37 defines such a method on an entirely new class. In the section Extension Methods, later in this chapter, we show how to make it appear as an instance method on DirectoryInfo.

## Static Constructors

In addition to static fields and methods, C# also supports static constructors. Static constructors are provided as a means to initialize a class (not the class instance). Static constructors are not called explicitly; instead, the runtime calls static constructors automatically upon first access to the class, whether via calling a regular constructor or accessing a static method or field on the class. You use static constructors to initialize the static data within the class to a particular value, mainly when the initial value involves more complexity than a simple assignment at declaration time. Consider Listing 5.38.

### LISTING 5.38: Declaring a Static Constructor

```
class Employee
{
    static Employee()
    {
        Random randomGenerator = new Random();
        NextId = randomGenerator.Next(101, 999);
    }

    // ...

    public static int NextId = 42;

    // ...
}
```

Listing 5.38 assigns the initial value of NextId to be a random integer between 100 and 1,000. Because the initial value involves a method call, the NextId initialization code appears within a static constructor and not as part of the declaration.

If assignment of NextId occurs within both the static constructor and the declaration, it is not obvious what the value will be when initialization concludes. The C# compiler generates CIL in which the declaration assignment is moved to be the first statement within the static constructor.

Therefore, NextId will contain the value returned by randomGenerator.Next(101, 999) instead of a value assigned during NextId's declaration. Assignments within the static constructor, therefore, will take precedence over assignments that occur as part of the field declaration, as was the case with instance fields. Note that there is no support for defining a static finalizer.

## ADVANCED TOPIC

### Favor Static Initialization during Declaration

Static constructors execute before the first access to any member of a class, whether it is a static field, another static member, or the constructor. In order to support this, the compiler injects a check into all type static members and constructors to ensure that the static constructor runs first.

Without the static constructor, the compiler instead initializes all static members to their default value and avoids adding the static constructor check. The result is for static assignment initialization to be called before accessing any static fields but not necessarily before all static methods or any instance constructor is invoked. This might provide a performance improvement if initialization of static members is expensive and not needed before accessing a static field.

## Static Properties

You also can declare properties as static. For example, Listing 5.39 wraps the data for the next ID into a property.

### LISTING 5.39: Declaring a Static Property

```
class Employee
{
 // ...
 public static int NextId
 {
 get
 {
 return _NextId;
 }
 private set
 {
 _NextId = value;
 }
}
```
