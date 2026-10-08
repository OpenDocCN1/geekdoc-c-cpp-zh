
corresponding parameter. Using named arguments, the different method calls in Listing 3.8 and the illegal call just shown could be written as shown in Listing 3.9.

### LISTING 3.9 Using Named Arguments

```
Search(latitude: 27.966667f, longitude: 82.533333f, distance: 3);
Search(latitude: 27.966667f, longitude: 82.533333f, distance: 3, culture: "en-GB");
Search(latitude: 27.966667f, longitude: 82.533333f);
Search(27.966667f, 82.533333f, culture: "en-GB");
Search(latitude: 27.966667f, longitude: 82.533333f, culture: "en-GB");
```

All these calls are equivalent. The first three calls are the same as the calls in Listing 3.8 except that each parameter is explicitly named. The last two calls show how we can omit an argument in the middle of the parameter list and are also the same, although one uses a mixture of named and positional arguments.

## By the Way

## Named and Positional Arguments

Arguments that are not passed by name are called positional arguments. Positional arguments are the most common.

Named arguments are most often used with optional parameters, but they can be used without them as well. Unlike optional parameters, named arguments can be used with value, reference, and output parameters. You can also use named arguments with parameter arrays, but you must explicitly declare a new array to contain the values, as shown here:

```
Console.WriteLine(String.Concat(values: new string[] { "a", "b", "c" }));
```

As you can see from the Search method, by enabling you to explicitly indicate the name of an argument, C# provides an additional (and powerful) way to help write fully describing and self-documenting code.

## Did you Know?

## Changing the Order of Arguments

Arguments are always evaluated in the order they are specified. Although not generally needed, named arguments enable you to change the order an argument appears in the invocation list:

```
Search(longitude: 82.533333f, latitude: 27.966667f);
Search(latitude: 27.966667f, longitude: 82.533333f);
```

## Try It Yourself

## Working with Optional Parameters and Named Arguments

To modify the Search methods previously defined to use optional parameters rather than overloads, follow these steps. If you closed Visual Studio, repeat the previous exercises first. Be sure to keep Visual Studio open at the end of this exercise because you will use this application later.

- 1. Open the `Contact.cs` file.
- 2. Remove the first two Search methods, leaving only the method containing all four parameters, and modify that method so that distance and culture are optional, using 10 and "en-US" as the default values.
- 3. Run the application using Ctrl+F5 and observe that the output matches what is shown in Figure 3.6.

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_101_0.png)

FIGURE 3.6 Working with optional parameters and named arguments

- 4. In the Main method of the Program.cs file, change the calls to the Search method to use different combinations of named parameters and observe the output after each change.

## Instantiating a Class

Unlike the predefined value types in which you could simply declare a variable and assign it a value, to use a class in your own programs, you must create an instance of that class.

Remember, even though you create new objects directly using the new keyword, the virtual execution system is responsible for actually allocating the memory required, and the garbage collector is responsible for deallocating that memory.

Instantiating a class is accomplished using the new keyword, like this:

```
Contact c = new Contact();
```

A newly created object must be given an initial state, which means any fields declared must be given an initial value either by explicitly providing one or accepting the default values (see Table 2.13 in Chapter 2).

Sometimes this level of initialization is sufficient, but often it won’t be. To provide additional actions that occur during initialization, C# provides an **instance constructor** (sometimes just called a constructor), which is a special method executed automatically when you create the instance.

A constructor has the same name of the class but it cannot return a value, which is different from a method that returns void. If the constructor has no parameters, it is the default constructor.

## By the Way

**Default Constructors**

Every class must have a constructor, but you don’t always have to write one. If you don’t include any constructors, the C# compiler creates a default constructor for you. This constructor won’t actually do anything, but it will be there.

Because the compiler only generates the default constructor if you don’t provide any additional constructors, it is easy to break the public interface of your class by adding an additional constructor that has parameters and forgetting to also explicitly add the default constructor. As a result, it is a good idea to always provide a default constructor rather than letting the compiler generate it for you.

The default constructor (or any constructor) can have any of the accessibility modifiers, so it is entirely possible to create a private default constructor. This is useful if you want to allow your class to be created but want to ensure that certain information is always provided when the object is instantiated.

Listing 3.10 shows the default constructor for the Contact class.

### LISTING 3.10 Declaring a Default Constructor

```
public class Contact
{
    public Contact()
    {
    }
}
```

Just as it is possible to overload regular methods, it is also possible to overload constructors. The signature for a constructor is the same as it is for a regular method, so the set of overloaded constructors must also vary by signature.

Some reasons for providing specialized constructors follow:

- ▶ There is no reasonable initial state without parameters.
- ▶ Providing an initial state is convenient and reasonable for the type.
- ▶ Constructing the object can be expensive, so you want to ensure that the object has the correct initial state when it is created.
- ▶ A non-public constructor restricts who can create objects using it.

Looking at the `Contact` class you have been using, it would certainly be useful if you provided values for the `firstName`, `lastName`, and `dateOfBirth` fields when creating a new instance. To do that, you would declare an overloaded constructor like the one shown in Listing 3.11.

### LISTING 3.11 Declaring a Constructor Overload

```
public class Contact
{
  public Contact(string firstName, string lastName, DateTime dateOfBirth)
  {
    this.firstName = firstName;
    this.lastName = lastName;
    this.dateOfBirth = dateOfBirth;
  }
}
```

In the constructor overload from Listing 3.11, you assigned the value of the parameter to its corresponding private field.

Typically, although not always, when a class contains multiple constructors, those constructors are chained together. To chain constructors together, you use a special syntax that uses the `this` keyword.

## The this Keyword

The `this` keyword refers to the current instance of the class. It is similar to the `Me` keyword in Visual Basic, a self identifier in F#, the `__self__` attribute in Python, and `self` in Ruby.

The common uses of `this` follow:

- ▶ To qualify members hidden by similar names
- ▶ To pass an object as a parameter to other methods
- ▶ To specify which constructor should be called from another constructor overload
- ▶ To indicate the extended type in an extension method

Because static members exist at the class level and are not associated with an instance, you can’t use the `this` keyword.

In Listing 3.11, the `this` keyword is used to distinguish between the class field and the parameter because both have the same name.

## By the Way

Listing 3.12 shows the Contact class with both constructors from Listing 3.10 and Listing 3.11 using constructor chaining.

### LISTING 3.12 Constructor Chaining

```
public class Contact
{
    public Contact()
    {
    }

    public Contact(string firstName, string lastName, DateTime dateOfBirth)
        : this()
    {
        this.firstName = firstName;
        this.lastName = lastName;
        this.dateOfBirth = dateOfBirth;
    }
}
```

One benefit of constructor chaining is that you can chain in any constructor provided by the class, not just the default constructor. When you use constructor chaining, it is important to understand the order in which the constructors execute. The constructor chain is followed until it reaches the last chained constructor, and then constructors will be executed in order going back out of the chain. Listing 3.13 shows a class, C, with three constructors, each chained through to the default constructor.

### LISTING 3.13 Chained Constructor Order of Execution

```
public class C
{
    string c1;
    string c2;
    int c3;

    public C()
    {
        Console.WriteLine("Default constructor");
    }

    public C(int i, string p1) : this(p1)
    {
        Console.WriteLine(i);
    }

    public C(string p1) : this()
    {
        Console.WriteLine(p1);
    }
}
```

Figure 3.7 shows the sequence in which each constructor would execute when instantiated using the second constructor (the one that takes an int and a string as input).
