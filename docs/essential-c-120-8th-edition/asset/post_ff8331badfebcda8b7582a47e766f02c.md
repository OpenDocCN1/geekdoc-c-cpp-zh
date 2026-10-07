
# 398 Chapter 7: Inheritance

virtual Modifier
# supports overriding on instance methods and properties but not on fields or on any static members. It requires an explicit action within both the base class and the derived class. The base class must mark each member for which it allows overriding as virtual. If public or protected members do not include the virtual modifier, subclasses will not be able to override those members.

## Language Contrast: Java—Virtual Methods by Default

By default, methods in Java are virtual, and they must be explicitly sealed if nonvirtual behavior is preferred. In contrast, C# defaults to nonvirtual.

Listing 7.9 shows an example of property overriding.

LISTING 7.9: Overriding a Property

```csharp
public class PdaItem
{
    public virtual string Name { get; set; }
    // ...
}
```

```csharp
public class Contact : PdaItem
{
    public override string Name
    {
        get
        {
            return $"{FirstName} {LastName}";
        }
        set
        {
            string[] names = value.Split(' ');
            // Error handling not shown
            FirstName = names[0];
            LastName = names[1];
        }
    }

    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

```csharp
// ...
}
```

Not only does PdaItem include the virtual modifier on the Name property, but Contact's Name property is also decorated with the keyword override. Eliminating virtual would result in an error and omitting override would cause a warning to be generated, as you will see shortly. C# requires the overriding methods to use the override keyword explicitly. In other words, virtual identifies a method or property as available for replacement (overriding) in the derived type.

## Language Contrast: Java and C++—Implicit Overriding

Unlike in Java and C++, the override keyword is required on the derived class in C#. C# does not allow implicit overriding. To override a method, both the base class and the derived class members must match and have corresponding virtual and override keywords. Furthermore, when the override keyword is specified, the derived implementation is assumed to replace the base class implementation.

Overriding a member causes the runtime to call the most derived implementation (see Listing 7.10 with Output 7.1).

## LISTING 7.10: Runtime Calling the Most Derived Implementation of a Virtual Method

```csharp
public class Program
{
    public static void Main()
    {
        Contact contact;
        PdaItem item;

        contact = new Contact();
        item = contact;

        // Set the name via PdaItem variable
        item.Name = "Inigo Montoya";

        // Display that FirstName & LastName
```

```csharp
// properties were set
Console.WriteLine(
  $contact.FirstName} {contact.LastName}"
)
```

# OUTPUT 7.1

Inigo Montoya

In Listing 7.10, when item.Name, which is declared on the PdaItem, is assigned, the contact’s FirstName and LastName are still set. The rule is that whenever runtime encounters a virtual method, it calls the most derived and overriding implementation of the virtual member. In this case, the code instantiates a Contact and calls Contact.Name because Contact contains the most derived implementation of Name.

Virtual methods provide default implementations only—that is, implementations that derived classes could override entirely. However, because of the complexities of inheritance design, it is important to consider (and preferably to implement) a specific scenario that requires the virtual method definition rather than to declare members as virtual by default.

This step is also important because converting a method from a virtual method to a nonvirtual method could break derived classes that override the method. Once a virtual member is published, it should remain virtual if you want to avoid introducing a breaking change. So be careful when introducing a virtual member—perhaps making it private protected, for example.

## Language Contrast: C++—Dispatch Method Calls during Construction

In C++, methods called during construction will not dispatch the virtual method. Instead, during construction, the type is associated with the base type rather than the derived type, and virtual methods call the base implementation. In contrast, C# dispatches virtual calls to the most derived type. This is consistent with the principle of calling the most derived virtual member, even if the derived constructor has not completely executed. Regardless, in C#, the situation should be avoided.

Finally, only instance members can be virtual. The CLR uses the concrete type.

## Covariant Types

Generally, the signature of the overriding method must match the signature of the base method. However, starting in C# 9.0, an improvement was made that allowed the overriding method to specify a return type different from the base method. This feature is called **covariant types**.

LISTING 7.11: Covariant Types

```csharp
public class Base
{
    public virtual Base Create() => new();
}

public class Derived : Base
{
    public override Derived Create() => new();
}
```

# Chapter 7: Inheritance

Notice how the Base class's Create() returns Base while the Derived class's returns Derived. Covariance will be discussed more in Chapter 12.

## Modifier

When an overriding method does not use override, the compiler issues a warning similar to that in Output 7.2 or 7.3.

# OUTPUT 7.2

```
warning CS014: '<derived method>' hides inherited member. To make current member override, add the override keyword.
```

# OUTPUT 7.3

```
warning CS008: The keyword new is required on '<derived property>' because it hides inherited member
```

The obvious solution is to add the override modifier (assuming the base member is virtual). However, as the warnings point out, the new modifier is also an option. Consider the scenario shown in Table 7.1—a specific example of the more general case known as the fragile base class problem.

## TABLE 7.1: Why the New Modifier

| Activity | Code |
| :--- | :--- |
| Programmer A defines class Person that includes properties FirstName and LastName | `public class Person {
  public string FirstName { get; set; }
  public string LastName { get; set; }
}` |
| Programmer B derives from Person and defines Contact with the additional property Name, In addition he defines the Program class whose Main() method instantiates Contact, and then prints out the name. | `public class Contact : Person {
  public string Name {
    get
    return FirstName + " " + LastName;
    set
      string[] names = value.Split(' ');
      // Error handling not shown
      FirstName = names[0];
      LastName = names[1];
  }
}` |
