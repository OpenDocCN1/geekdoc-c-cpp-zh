# ## Parameterless Constructors

A constructor can take parameters just like any other method to help it in its setup tasks. A *parameterless constructor* (sometimes called an *empty constructor*) takes no parameters, so it's somewhat limited in what it can do.

For example, suppose the `Manager` class has a `DirectReports` property, which is a list of `Employee`s that report to a given manager. A parameterless constructor cannot build that list because it doesn't know what employees to put in it. It can, however, initialize the `DirectReports` property to an empty list, as shown in the following code:

```
~~~csharp
class Manager : Employee
{
    public List<Employee> DirectReports;

    // Initialize the Manager.
    public Manager()
    {
        DirectReports = new List<Employee>();
    }
}
~~~
```

You implicitly invoke a parameterless constructor any time you create an object without using any parameters. For example, the following code creates a new `Person` object. When this code executes, control jumps briefly to the parameterless constructor so it can prepare the object for use.

```
~~~csharp
Manager fred = new Manager();
~~~
```

Note that C# creates a default public parameterless constructor for you if you don't define any constructors explicitly. If you give the class any constructors, however, C# doesn't create the default constructor. In that case, if you want a parameterless constructor, you must make it yourself.

# ## Parameterized Constructors

Parameterless constructors are useful but fairly limited because they don't have much information to go by. To give a constructor more information, you can make it take parameters just like you can with any other method.

One simple type of parameterized constructor uses its parameters to initialize properties. For example, you could make a constructor for the `Person` class that takes the person's first and last names as parameters. The constructor could then set the object's `FirstName` and `LastName` properties.

Why would you bother doing this when you could use an initializer? First, the syntax for using a constructor is slightly more concise than initializer syntax. The following code uses a constructor that takes eight parameters to initialize an `Employee`'s properties:

```
~~~csharp
Employee alice = new Employee("Alice", "Archer", "100 Ash Ave",
    "Bugsville", "CO", "82010", 1001, "A-1");
~~~
```

Compare this code to the earlier snippet that used initializers. This version is more concise, although it's less self-documenting because it doesn't explicitly list the property names.