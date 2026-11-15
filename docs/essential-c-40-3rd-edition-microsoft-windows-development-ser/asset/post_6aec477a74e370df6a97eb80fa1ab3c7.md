
for the derived class, but the implementation is not always valid. There needs to be a mechanism for **overriding** the base class implementation with a custom implementation in the derived class.

## virtual Modifier

C# supports overriding on instance methods and properties but not on fields or any static members. It requires an explicit action within both the base class and the derived class. The base class must mark each member for which it allows overriding as virtual. If public or protected members do not include the virtual modifier, then subclasses will not be able to override those members.

> ## Language Contrast: Java—Virtual Methods by Default
>
> By default, methods in Java are virtual, and they must be explicitly sealed if nonvirtual behavior is preferred. In contrast, C# defaults to nonvirtual.

Listing 6.10 shows an example of property overriding.

## LISTING 6.10: Overriding a Property

```
public class PdAItem
{
    public virtual string Name { get; set; }
    // ...
}

public class Contact : PdAItem
{
    public override string Name
    {
        get
        {
            return FirstName + " " + LastName;
        }
        set
        {
            string[] names = value.Split(' ');
            // Error handling not shown.
            FirstName = names[0];
            LastName = names[1];
        }
    }
}
} }
public string FirstName { get; set; }
public string LastName { get; set; }
// ...
}
```

Not only does PdAItem include the virtual modifier on the Name property, but also Contact's Name property is decorated with the keyword override. Eliminating virtual would result in an error and omitting override would cause a warning, as you will see shortly. C# requires the overriding methods to use the override keyword explicitly.

In other words, virtual identifies a method or property as available for replacement (overriding) in the derived type.

> ## Language Contrast: Java and C++—Implicit Overriding
>
> Unlike with Java and C++, the override keyword is required on the derived class. C# does not allow implicit overriding. In order to override a method, both the base class and the derived class members must match and have corresponding virtual and override keywords. Furthermore, if specifying the override keyword, the derived implementation is assumed to replace the base class implementation.

Overriding a member causes the runtime to call the most derived implementation (see Listing 6.11).

## LISTING 6.11: Runtime Calling the Most Derived Implementation of a Virtual Method

```
public class Program
{
public static void Main()
{
Contact contact;
PdAItem item;
contact = new Contact();
item = contact;
// Set the name via PdaItem variable
item.Name = "Inigo Montoya";

// Display that FirstName & LastName
// properties were set.
Console.WriteLine("{0} {1}",
    contact.FirstName, contact.LastName);
}
```

Output 6.1 shows the results of Listing 6.11.

## Output 6.1:

Inigo Montoya

In Listing 6.11, item.Name is called, where item is declared as a PdAItem. However, the contact's FirstName and LastName are still set. The rule is that whenever the runtime encounters a virtual method, it calls the most derived and overriding implementation of the virtual member. In this case, the code instantiates a Contact and calls Contact.Name because Contact contains the most derived implementation of Name.

In creating a class, programmers should be careful when choosing to allow overriding a method, since they cannot control the derived implementation. Virtual methods should not include critical code because such methods may never be called if the derived class overrides them. Furthermore, converting a method from a virtual method to a nonvirtual method could break derived classes that override the method. This is a code-breaking change and you should avoid it, especially for assemblies intended for use by third parties.

Listing 6.12 includes a virtual Run() method. If the Controller programmer calls Run() with the expectation that the critical Start() and Stop() methods will be called, he will run into a problem.

## LISTING 6.12: Carelessly Relying on a Virtual Method Implementation

```
public class Controller
{
    public void Start()
    {
        // Critical code
}
public virtual void Run()
{
    Start();
    Stop();
}
public void Stop()
{
    // Critical code
}
}
```

In overriding Run(), a developer could perhaps not call the critical Start() and Stop() methods. To force the Start()/Stop() expectation, the Controller programmer should define the class, as shown in Listing 6.13.

## LISTING 6.13: Forcing the Desirable Run() Semantics

```
public class Controller
{
    public void Start()
    {
        // Critical code
    }

    private void Run()
    {
        Start();
        InternalRun();
        Stop();
    }

    protected virtual void InternalRun()
    {
        // Default implementation
    }

    public void Stop()
    {
        // Critical code
    }
}
```

With this new listing, the Controller programmer prevents users from wantonly calling InternalRun(), because it is protected. On the other hand, declaring Run() as public ensures that Start() and Stop() are invoked appropriately. It is still possible for users to modify the default implementation of how the Controller executes by overriding the protected InternalRun() member from within the derived class.

Virtual methods provide default implementations only, implementations that derived classes could override entirely. However, because of the complexities of inheritance design, it is important to consider (and preferably to implement) a specific scenario that requires the virtual method definition.

## Language Contrast: C++ — Dispatch Method Calls during Construction

In C++, methods called during construction will not dispatch the virtual method. Instead, during construction, the type is associated with the base type rather than the derived type, and virtual methods call the base implementation. In contrast, C# dispatches virtual method calls to the most derived type. This is consistent with the principle of calling the most derived virtual member, even if the derived constructor has not completely executed. Regardless, in C# the situation should be avoided.

Finally, only instance members can be virtual. The CLR uses the concrete type, specified at instantiation time, to determine where to dispatch a virtual method call, so static virtual methods are meaningless and the compiler prohibits them.

## new Modifier

When an overriding method does not use override, the compiler issues a warning similar to that shown in Output 6.2 or Output 6.3.

## Output 6.2:

```
warning CS0114: '<derived method name>' hides inherited member '<base method name>'. To make the current member override that implementation, add the override keyword. Otherwise add the new keyword.
```

## Output 6.3:

```
warning CS0108: The keyword new is required on '<derived property name>' because it hides inherited member '<base property name>'
```

The obvious solution is to add the override modifier (assuming the base member is virtual). However, as the warnings point out, the new modifier is also an option. Consider the scenario shown in Table 6.1—a specific example of the more general problem known as the brittle base class or fragile base class problem.

## TABLE 6.1: Why the New Modifier?

| Activity | Code |
| :--- | :--- |
| Programmer A defines class Person that includes properties FirstName and LastName. | `public class Person
{
    public string FirstName { get; set; }
    public string LastName { get; set; }
}` |
| Programmer B derives from Person and defines Contact with the additional property Name. In addition, he defines the Program class whose Main() method instantiates Contact, assigns Name, and then prints out the name. | `public class Contact : Person
{
    public string Name
    {
        get
        {
            return FirstName + " " + LastName;
        }
        set
        {
            string[] names = value.Split(' ');
            // Error handling not shown.
            FirstName = names[0];
            LastName = names[1];
        }
    }
}` |
