
## TABLE 6.1: Why the New Modifier? (Continued)

| Activity | Code |
| :--- | :--- |
| Later, Programmer A adds the Name property, but instead of implementing the getter as FirstName + " " + LastName, she implements it as LastName + ", " + FirstName. Furthermore, she doesn't use virtual as a property, and she uses the property in a DisplayName() method. | public class Person
{
    public string Name
    {
        get
        {
            return LastName + ", " + FirstName;
        }
        set
        {
            string[] names = value.Split(';');
            // Error handling not shown.
            LastName = names[0];
            FirstName = names[1];
        }
    }
    public static void Display(Person person)
    {
        // Display <LastName>, <FirstName>
        Console.WriteLine( person.Name );
    }
} |

Because Person.Name is not virtual, Programmer A will expect Display() to use the Person implementation, even if a Person-derived data type, Contact, is passed in. However, Programmer B would expect Contact.Name to be used in all cases where the variable data type is a Contact. (Programmer B would have no code where Person.Name was used, since no Person.Name property existed initially.) To allow the addition of Person.Name without breaking either programmer's expected behavior, you cannot assume virtual was intended. Furthermore, since C# requires an override member to explicitly use the override modifier, some other semantic must be assumed, instead of allowing the addition of a member in the base class to cause the derived class to no longer compile.

The semantic is the new modifier, and it hides a redeclared member of the derived class from the base class. Instead of calling the most derived member, a member of the base class calls the most derived member in the inheritance chain prior to the member with the new modifier. If the inheritance chain contains only two classes, then a member in the base class will behave as though no method was declared on the derived class (if the derived implementation overrides the base class member). Although the compiler will report the warning shown in either Output 6.2 or Output 6.3, if neither override nor new is specified, then new will be assumed, thereby maintaining the desired version safety.

Consider Listing 6.14, for example. Its output appears in Output 6.4.

## LISTING 6.14: override versus new Modifier

```
public class Program
{
    public class BaseClass
    {
        public void DisplayName()
        {
            Console.WriteLine("BaseClass");
        }
    }

    public class DerivedClass : BaseClass
    {
        // Compiler WARNING: DisplayName() hides inherited
        // member. Use the new keyword if hiding was intended.
        public virtual void DisplayName()
        {
            Console.WriteLine("DerivedClass");
        }
    }

    public class SubDerivedClass : DerivedClass
    {
        public override void DisplayName()
        {
            Console.WriteLine("SubDerivedClass");
        }
    }

    public class SuperSubDerivedClass : SubDerivedClass
    {
        public new void DisplayName()
        {
            Console.WriteLine("SuperSubDerivedClass");
        }
    }

    public static void Main()
    {
        SuperSubDerivedClass superSubDerivedClass
            = new SuperSubDerivedClass();
        SubDerivedClass subDerivedClass = superSubDerivedClass;
        DerivedClass derivedClass = superSubDerivedClass;
        BaseClass baseClass = superSubDerivedClass;

        superSubDerivedClass.DisplayName();
        subDerivedClass.DisplayName();
        derivedClass.DisplayName();
        baseClass.DisplayName();
    }
}
```

```
OUTPUT 6.4:

SuperSubDerivedClass
SubDerivedClass
DerivedClass
BaseClass
```

These results occur for the following reasons.

- SuperSubDerivedClass: SuperSubDerivedClass.DisplayName() displays SuperSubDerivedClass because there is no derived class and hence, no overload.
- SubDerivedClass: SubDerivedClass.DisplayName() is the most derived member to override a base class's virtual member. SuperSubDerivedClass.DisplayName() is hidden because of its new modifier.
- SubDerivedClass: DerivedClass.DisplayName() is virtual and SubDerivedClass.DisplayName() is the most derived member to override it. As before, SuperSubDerivedClass.DisplayName() is hidden because of the new modifier.
- BaseClass: BaseClass.DisplayName() does not redeclare any base class member and it is not virtual; therefore, it is called directly.

When it comes to the CIL, the new modifier has no effect on what statements the compiler generates. However, a “new” method results in the generation of the newslot metadata attribute on the method. From the C# perspective, its only effect is to remove the compiler warning that would appear otherwise.

## sealed Modifier

Just as you can prevent inheritance using the sealed modifier on a class, virtual members may be sealed, too (see Listing 6.15). This prevents a sub-class from overriding a base class member that was originally declared as virtual higher in the inheritance chain. The situation arises when a subclass B overrides a base class A's member and then needs to prevent any further overriding below subclass B.

## LISTING 6.15: Sealing Members

```
class A
{
    public virtual void Method()
    {
    }
}

class B : A
{
    public override sealed void Method()
    {
    }
}

class C : B
{
    // ERROR: Cannot override sealed members
    // public override void Method()
    // {
    // }
}
```

In this example, the use of the sealed modifier on class B's Method() declaration prevents C's overriding of Method().

## base Member

In choosing to override a member, developers often want to invoke the member on the base class (see Listing 6.16).

## LISTING 6.16: Accessing a Base Member

```
public class Address
{
    public string StreetAddress;
    public string City;
    public string State;
    public string Zip;

    public override string ToString()
    {
        return string.Format("{0}" + Environment.NewLine +
            "{1}, {2} {3}",
            StreetAddress, City, State, Zip);
    }
}

public class InternationalAddress : Address
{
    public string Country;

    public override string ToString()
    {
        return base.ToString() + Environment.NewLine +
            Country;
    }
}
```

In Listing 6.16, InternationalAddress inherits from Address and implements ToString(). To call the parent class's implementation you use the base keyword. The syntax is virtually identical to this, including support for using base as part of the constructor (discussed shortly).

Parenthetically, in the Address.ToString() implementation, you are required to override as well because ToString() is also a member of object. Any members that are decorated with override are automatically designated as virtual, so additional child classes may further specialize the implementation.

## Constructors

When instantiating a derived class, the runtime first invokes the base class's constructor so that the base class initialization is not circumvented. However, if there is no accessible (nonprivate) default constructor on the base class, then it is not clear how to construct the base class and the C# compiler reports an error.

To avoid the error caused by no accessible default constructor, programmers need to designate explicitly, in the derived class constructor header, which base constructor to run (see Listing 6.17).

## LISTING 6.17: Specifying Which Base Constructor to Invoke

```
public class PdaItem
{
    public PdaItem(string name)
    {
        Name = name;
    }

    // ...
}

public class Contact : PdaItem
{
    public Contact(string name) :
        base(name)
    {
        Name = name;
    }

    public string Name { get; set; }

    // ...
}
```

By identifying the base constructor in the code, you let the runtime know which base constructor to invoke before invoking the derived class constructor.

## Abstract Classes

Many of the inheritance examples so far have defined a class called PdaItem that defines the methods and properties common to Contact, Appointment, and so on, which are type objects that derive from PdaItem. PdaItem is not intended to be instantiated itself, however. A PdaItem instance has no meaning by itself; it has meaning only when it is used as a base class—to share default method implementations across the set of data types that derive from it. These characteristics are indicative of the need for PdaItem to be an abstract class rather than a concrete class. Abstract classes are designed for derivation only. It is not possible to instantiate an abstract class, except in the context of instantiating a class that derives from it. Classes that are not abstract and can instead be instantiated directly are concrete classes.
