
# Language Contrast: Java—Inner Classes

Java includes not only the concept of a nested class but also the concept of an inner class. Inner classes correspond to objects that are associated with the containing class instance, rather than just a syntactic relationship. In C#, you can achieve the same structure by including an instance field of a nested type within the outer class. A factory method or constructor can ensure a reference to the corresponding instance of the outer class is set within the inner class as well.

# Partial Classes

Partial classes¹⁶ are portions of a class that the compiler can combine to form a complete class. Although you could define two or more partial classes within the same file, the general purpose of a partial class is to allow the splitting of a class definition across multiple files. Primarily this is useful for tools that are generating or modifying code. With partial classes, the tools can work on a file separate from the one the developer is manually coding.

# Defining a Partial Class

C# allows declaration of a partial class by prepending a contextual keyword, partial, immediately before class,¹⁷ as Listing 6.57 shows.

LISTING 6.57: Defining a Partial Class

```
// File: Program1.cs
partial class Program
{
}
// File: Program2.cs
partial class Program
{
}
```

16. Introduced with C# 2.0.
17. Interfaces (Chapter 8) structs (Chapter 9) can also be partial.

In this case, each portion of Program is placed into a separate file, as identified by the comment.

Besides their use with code generators, another common use of partial classes to place any nested classes into their own files. This is in accordance with the coding convention that places each class definition within its own file. For example, Listing 6.58 places the Program.CommandLine class into a file separate from the core Program members.

# Listing 6.58: Defining a Nested Class in a Separate Partial Class

```
// File: Program.cs
partial class Program
{
    static void Main(string[] args)
    {
        CommandLine CommandLine = new(args);

        switch (CommandLine.Action)
        {
            // ...
        }
    }
}
// File: Program+CommandLine.cs
partial class Program
{
    // Define a nested class for processing the command line
    private class CommandLine
    {
        // ...
    }
}
```

Partial classes do not allow for extending compiled classes or classes in other assemblies. They are simply a means of splitting a class implementation across multiple files within the same assembly.

# Partial Classes

# Partial Methods

Extending the concept of partial classes is the concept of partial methods,¹8 which are allowed only within partial types. Like partial classes, their primary purpose is to accommodate code generation.

Consider a code generation tool that generates the Person.Designer.cs file for the Person class based on a Person table in the database. This tool examines the table and creates properties for each column in the table. The problem, however, is that frequently the tool cannot generate any validation logic that may be required because of business rules that are not embedded into the database definition. To overcome this difficulty, the developer of the Person class needs to add the validation logic. It is undesirable to modify Person.Designer.cs directly, because if it is regenerated (to accommodate an additional column in the database), the changes would be lost. Instead, the structure of the code for Person needs to be separated out so that the generated code appears in one file, and the custom code (with business rules) is placed into a separate file, unaffected by any regeneration. As we saw in the preceding section, partial classes are well suited for the task of splitting a class across multiple files, but they are not always sufficient. In many cases, we also need partial methods.

Partial methods allow for a declaration of a method without requiring an implementation. However, when the optional implementation is included, it can be located in one of the sister partial class definitions—likely in a separate file. Listing 6.59 shows the partial method declaration and the implementation for the Person class.

+   Listing 6.59: Defining a Partial Method to Access Its Implementation

```
// File: Person.Designer.cs
public partial class Person
{
    #region Extensibility Method Definitions
    static partial void OnLastNameChanging(string value);
    static partial void OnFirstNameChanging(string value);
    #endregion Extensibility Method Definitions
```

18. Introduced with C# 3.0.

# Chapter 6: Classes

```
// ...
public string LastName
{
    get {
        return _LastName;
    }
    set {
        if (_LastName != value) {
            OnLastNameChanging(value);
            _LastName = value;
        }
    }
}
private string _LastName;

// ...
public string FirstName
{
    get {
        return _FirstName;
    }
    set {
        if (_FirstName != value) {
            OnFirstNameChanging(value);
            _FirstName = value;
        }
    }
}
private string _FirstName;
public partial string GetName();

// File: Person.cs
partial class Person
{
    static partial void OnLastNameChanging(string value)
    {
        value = value ??
            throw new ArgumentNullException(nameof(value));
    }
}
```

# Partial Classes 383

```
if (value.Trim().Length == 0)
{
    throw new ArgumentException(
        "{nameof(LastName)} cannot be empty.",
        nameof(value));
}

//...
public partial string GetName() => $"{FirstName} {LastName}";
```

In the listing of Person.Designer.cs are declarations for the LastNameChanging() and OnFirstNameChanging(). Furthermore, the properties for the last and first names make calls to their changing methods. Even though the declarations contain no implementation, this code will successfully compile. The key is that the methods are prefixed with contextual keyword partial. In Listing 6.59, only the LastNameChanging() method is implemented. In this case, the implementation checks the suggested LastName value and throws an exception if it is not valid. Notice that the signatures for LastNameChanging() between the two locations match.

Prior to C# 9.0, partial methods must return void. If the method didn't return void and the implementation was not provided, what would the expected return from a call to a non-implemented method? To avoid any assumptions about the return, C# designers decided to prohibit methods with returns other than void. Similarly, out parameters are not allowed on partial methods. If a return value is required, ref parameters may be used. Lastly, partial members cannot be decorated with an accessibility modifier (e.g., private or public). Rather, partial methods are implicitly private.

Starting with C# 9.0, these restrictions were all removed. Partial methods could return values, have out parameters, and even have access modifiers. In fact, distinguishing this unrestricted version of a partial method, C# required the access modifier, even for methods that were intended to be private. To remove the

![](img/ffe0f34eac7523830420733690014d7_417_0.png)

# 384 Chapter 6: Classes

restrictions

In summary, partial methods allow generated code to call methods that have not necessarily been implemented. Furthermore, if no implementation is provided for a partial method, no trace of the partial method appears in the Cil. This helps keep code size small while keeping flexibility high.

# Summary

This chapter explained C# constructs for classes and object orientation in C#. Its coverage included a discussion of declaring fields and how to access them on a class instance.

This chapter also discussed the key decision of whether to store data on a per-instance basis or across all instances of a type. Static data is associated with the class, whereas instance data is stored on each object.

In addition, the chapter explored encapsulation in the context of access modifiers for methods and data. The C# construct of properties was introduced, and you saw how to use it to encapsulate private fields.

The next chapter focuses on how to associate classes with each other inheritance and explores the benefits derived from this object-oriented construct.
