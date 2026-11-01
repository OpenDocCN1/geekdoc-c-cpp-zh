
The first line of the definition is the bit that is very similar to a field definition. The difference is that there is no semicolon at the end of the line; instead, you have a code block containing nested get and set blocks.

get blocks must have a return value of the type of the property. Simple properties are often associated with a single private field controlling access to that field, in which case the get block can return the field's value directly:

```
// Field used by property.
private int myInt;
// Property.
public int MyIntProp
{
    get { return myInt; }
    set { // Property set code. }
}
```

Code external to the class cannot access this myInt field directly due to its accessibility level (it is private). Instead, external code must use the property to access the field. The set function assigns a value to the field similarly. Here, you can use the keyword value to refer to the value received from the user of the property:

```
// Field used by property.
private int myInt;
// Property.
public int MyIntProp
{
    get { return myInt; }
    set { myInt = value; }
}
```

value equates to a value of the same type as the property, so if the property uses the same type as the field, then you never have to worry about casting in situations like this.

This simple property does little more than shield direct access to the myInt field. The real power of properties is apparent when you exert a little more control over the proceedings. For example, you might implement your set block as follows:

```
set
{
    if (value >= 0 && value <= 10)
        myInt = value;
}
```

Here, you modify myInt only if the value assigned to the property is between 0 and 10. In situations like this, you have an important design choice to make. What should you do if an invalid value is used? You have four options:

- Do nothing (as in the preceding code).
- Assign a default value to the field.
- Continue as if nothing went wrong but log the event for future analysis.
- Throw an exception.

Alternatively, you could hide the base class method:

```csharp
public class MyBaseClass
{
    public virtual void DoSomething() => WriteLine("Base imp");
}
public class MyDerivedClass : MyBaseClass
{
    new public void DoSomething() => WriteLine("Derived imp");
}
```

The base class method needn't be virtual for this to work, but the effect is exactly the same and the preceding code only requires changes to one line. The result for a virtual or nonvirtual base class method is as follows:

```
Base imp
```

Although the base implementation is hidden, you still have access to it through the base class.

## Calling Overridden or Hidden Base Class Methods

Whether you override or hide a member, you still have access to the base class member from the derived class. There are many situations in which this can be useful, such as the following:

- When you want to hide an inherited public member from users of a derived class but still want access to its functionality from within the class
- When you want to add to the implementation of an inherited virtual member rather than simply replace it with a new overridden implementation

To achieve this, you use the `base` keyword, which refers to the implementation of the base class contained within a derived class (in a similar way to its use in controlling constructors, as shown in the last chapter):

```csharp
public class MyBaseClass
{
    public virtual void DoSomething()
    {
        // Base implementation.
    }
}
public class MyDerivedClass : MyBaseClass
{
    public override void DoSomething()
    {
        // Derived class implementation, extends base class implementation.
        base.DoSomething();
        // More derived class implementation.
    }
}
```

This code executes the version of DoSomething() contained in MyBaseClass, the base class of MyDerivedClass, from within the version of DoSomething() contained in MyDerivedClass. As base works using object instances, it is an error to use it from within a static member.

To instantiate MyNestedClass from outside MyClass, you must qualify the name, as shown here:

```
MyClass.MyNestedClass myObj = new MyClass.MyNestedClass();
```

However, you might not be able to do this, for example if the nested class is declared as private. One reason for the existence of this feature is to define classes that are private to the containing class so that no other code in the namespace has access to them. Another reason is that nested classes have access to private and protected members of their containing class. The next Try it Out examines this feature.

## TRY IT OUT  Using Nested Classes: Ch10Ex02

1. Create a new console application called Ch10Ex02 and save it in the directory C:\BegVCSharp\Chapter10.
2. Modify the code in Program.cs as follows:

```
namespace Ch10Ex02
{
    public class ClassA
    {
        private int state = -1;
        public int State
        {
            get { return state; }
        }
        public class ClassB
        {
            public void SetPrivateState(ClassA target, int newState)
            {
                target.state = newState;
            }
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            ClassA myObject = new ClassA();
            WriteLine($"myObject.State = {myObject.State}");
            ClassA.ClassB myOtherObject = new ClassA.ClassB();
            myOtherObject.SetPrivateState(myObject, 999);
            WriteLine($"myObject.State = {myObject.State}");
            ReadKey();
        }
    }
}
```

is equivalent to:

```
public class MyClass : IMyInterface1, IMyInterface2 { ... }
```

Partial class definitions can include a base class in a single partial class definition, or more than one partial class definition. If a base class is specified in more than one definition, though, it must be the same base class; recall that classes in C# can inherit only from a single base class.

## PARTIAL METHOD DEFINITIONS

Partial classes can also define partial methods. Partial methods are defined in one partial class definition without a method body, and implemented in another partial class definition. In both places, the partial keyword is used:

```
public partial class MyClass
{
    partial void MyPartialMethod();
}
public partial class MyClass
{
    partial void MyPartialMethod()
    {
        // Method implementation
    }
}
```

Partial methods can also be static, but they are always private and can't have a return value. Any parameters they use can't be out parameters, although they can be ref parameters. They also can't use the virtual, abstract, override, new, sealed, or extern modifiers.

Given these limitations, it is not immediately obvious what purpose partial methods fulfill. In fact, they are important when it comes to code compilation, rather than usage. Consider the following code:

```
public partial class MyClass
{
    partial void DoSomethingElse();
    public void DoSomething()
    {
        WriteLine("DoSomething() execution started.");
        DoSomethingElse();
        WriteLine("DoSomething() execution finished.");
    }
}
public partial class MyClass
{
    partial void DoSomethingElse() =>
        WriteLine("DoSomethingElse() called.");
}
```

Here, the partial method DoSomethingElse() is defined and called in the first partial class definition, and implemented in the second. The output, when DoSomething() is called from a console application, is what you might expect:

```
DoSomething() execution started.
DoSomethingElse() called.
DoSomething() execution finished.
```

If you were to remove the second partial class definition or partial method implementation entirely (or comment out the code), the output would be as follows:

```
DoSomething() execution started.
DoSomething() execution finished.
```

You might assume that what is happening here is that when the call to DoSomethingElse() is made, the runtime discovers that the method has no implementation and therefore continues executing the next line of code. What actually happens is a little subtler. When you compile code that contains a partial method definition without an implementation, the compiler actually removes the method entirely. It also removes any calls to the method. When you execute the code, no check is made for an implementation because there is no call to check. This results in a slight — but nevertheless significant — improvement in performance.

As with partial classes, partial methods are useful when it comes to customizing autogenerated or designer-created code. The designer may declare partial methods that you can choose to implement or not depending on the situation. If you don't implement them, you incur no performance hit because effectively the method does not exist in the compiled code.

Consider at this point why partial methods can't have a return type. If you can answer that to your own satisfaction, you can be sure that you fully understand this topic — so that is left as an exercise for you.

## EXAMPLE APPLICATION

To illustrate some of the techniques you've been using so far, in this section you'll develop a class module that you can build on and make use of in subsequent chapters. The class module contains two classes:

- Card — Representing a standard playing card, with a suit of club, diamond, heart, or spade, and a rank that lies between ace and king
- Deck — Representing a full deck of 52 cards, with access to cards by position in the deck and the capability to shuffle the deck

You'll also develop a simple client to ensure that things are working, but you won't use the deck in a full card game application — yet.

## Planning the Application

The class library for this application, Ch10CardLib, will contain your classes. Before you get down to any code, though, you should plan the required structure and functionality of your classes.
