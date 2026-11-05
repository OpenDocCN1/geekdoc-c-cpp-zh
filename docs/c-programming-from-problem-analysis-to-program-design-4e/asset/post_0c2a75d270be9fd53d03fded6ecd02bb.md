
In Chapter 9, you wrote your first real Windows-based application and learned how easy it is to develop graphical user interfaces using C# and Visual Studio’s drag-and-drop construction approach. In addition, you learned that included as part of the .NET Framework `class` library are a number of predefined classes located in the `System.Windows.Forms` namespace that enable you to add controls such as `Label`, `Button`, and `TextBox` objects to an object of the Windows Form container class. And, finally, you learned a new way of programming based on interactively responding to events such as button clicks.

In this chapter, you will extend this knowledge by writing additional event-handling methods for capturing and responding to user input. You will create applications that have menus and other widgets such as list boxes, radio buttons, combo boxes, and check boxes that can be displayed and responded to. You will explore other types of events that are triggered or raised for Windows applications.

This chapter begins by introducing you to delegates. An understanding of their use makes you more aware of what goes on behind the scenes with events. The remainder of the chapter focuses on adding controls to Windows applications and programming their events. By the time you complete this chapter, you will be creating very sophisticated, highly interactive, Windows-based applications.

## Delegates

Delegates form the foundation for events in C#. **Delegates** are special types of .NET classes whose instances store references (addresses) to methods as opposed to storing actual data. You are used to passing data into methods through the use of parameters. Delegates enable you to pass methods as parameters into other methods. Delegates are used in applications other than Windows applications that respond to GUI events; however, it is their relationship to events that makes them interesting and worth presenting in this section.

### Defining Delegates

The `delegate` base class type is defined in the `System` namespace. A couple of syntactical differences exist between delegates and the other predefined and user-defined classes that you have already used. First, the declaration for a delegate looks more like a method declaration than a class definition; however, it has no body. It begins with the keyword `delegate` and it ends with a parenthesized list of parameters followed by a semicolon. Every `delegate` type has a signature, which may include zero or more parameters. Remember that a **signature** for a method includes its name, number of parameters, and parameter types. The signature of a method does not include the `return` type. Like methods, a delegate may include a `return` type or the keyword `void` as part of its heading. However, unlike a method, the `return` type of a delegate becomes part of its identifying signature. Example 10-1 defines a delegate type that takes no arguments and returns a `string`.

**Example 10.1**

```csharp
delegate string ReturnsSimpleString( );
```

When you define a `delegate` type, you identify what types of methods the `delegate` represents. This identification is accomplished through the `delegate` signature, which is very important. It indicates what the method signatures must look like if they are to be referenced by the `delegate`.

> **NOTE**
>
> In C#, you can think of the `delegate` as a way of defining or naming a method signature.

Given the signature for the `delegate` defined in Example 10-1, any method that has zero parameters and returns a `string` could be referenced by the `ReturnsSimpleString` `delegate`. Example 10-2 shows the heading and body for a prospective method.

**Example 10.2**

```csharp
// Method that returns a string.
static string EndStatement( )
{
    return " in 10 years.";
}
```

Compare the heading for the `EndStatement( )` method shown in Example 10-2 with the `delegate` in Example 10-1. Both return strings. Both have zero parameters. The `delegate` does not specify what the statements must be in the body of the method, and it does not specify what the name of the method must be, just what the signature must look like.

> **NOTE**
>
> A `delegate` is implemented in C# as a `class`; however, an instance of the `delegate` class is also referred to as a `delegate`, rather than as an object. The fact that both the `class` type and the instance type go by the same name can be confusing.

### Creating Delegate Instances

To associate the `delegate` with the method, a `delegate` instance is defined using the method name as the argument inside the parentheses. One way you have previously identified methods from field and property instances is by recognizing that the method name identifier is followed by a set of parentheses. When you write a method name without parentheses, you are referencing the address of the method. Example 10-3 instantiates the `ReturnsSimpleString` delegate with the `EndStatement()` method as the argument.

**Example 10.3**

```csharp
ReturnsSimpleString saying3 = new ReturnsSimpleString(EndStatement);
```

> **NOTE** The constructor for a `delegate` of the `delegate` class always takes just one parameter. This is because you are sending the name of a method for the constructor to reference.

Notice that the `EndStatement` argument does not include the parentheses, even though `EndStatement` is a method. A reference to the address of the method is sent as an argument. The address stored is the entry point in memory where the method begins when it is called.

### Using Delegates

After completing the instantiation in Example 10-3, the `delegate` identifier `saying3` references the `EndStatement()` method. Any use of `saying3()` calls the `EndStatement()` method. Example 10-4 illustrates this.

**Example 10.4**

```csharp
MessageBox.Show(saying3());
```

A call to the `Show()` method of the `MessageBox` class calls the `delegate` instance, `saying3()`, which calls the `EndStatement()` method to display “in 10 years.” Calling the `EndStatement()` method in the `Show()` method produces the same output. This is a simple example, but illustrates how a `delegate` is used to call a method. Example 10-4 did not directly call the `EndStatement()` method; however, the statements from its body were those executed.

> **NOTE** Recall that you must add a reference to `System.Windows.Forms` in order to use the `MessageBox.Show()` method. You access the **Reference Manager** from the **Solution Explorer** window. To avoid fully qualifying the name with your program statements, you should also add another `using` statement,
>
> `using System.Windows.Forms;`

The program in Example 10-5 illustrates defining a single `delegate` type, instantiating three `delegate` instances, and calling up the three delegates. Without looking closely, the arguments to the `Show( )` method appear to be normal method calls. In reality, the methods are called through the delegates. Notice that the `delegate` instance name and a set of parentheses form the argument to the `Show( )` method.

**Example 10.5**

```csharp
// DelegateExample.cs             Author: Doyle
// After defining a delegate class, three delegate
// instances are instantiated. Delegates are
// used as arguments for the Show( ) method.

using System;
using System.Windows.Forms;

namespace DelegateExample
{
    delegate string ReturnsSimpleString( );

    class DelegateExample
    {
        static void Main ( )
        {
            int age = 18;
            ReturnsSimpleString saying1 =
                new ReturnsSimpleString(AHeading);
            ReturnsSimpleString saying2 =
                new ReturnsSimpleString((age + 10).ToString);
            ReturnsSimpleString saying3=
                new ReturnsSimpleString(EndStatement);
            MessageBox.Show(saying1( ) +
                saying2( ) + saying3( ));
        }

        // Method that returns a string.
        static string AHeading()
        {
            return "Your age will be ";
        }

        // Method that returns a string.
        static string EndStatement( )
        {
            return " in 10 years.";
        }
    }
}
```
