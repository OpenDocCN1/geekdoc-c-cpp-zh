
## Parameter Declaration

Consider the declaration of the `DisplayGreeting()` and `GetFullName()` methods. The text that appears between the parentheses of a method declaration is the **parameter list**. Each parameter in the parameter list includes the type of the parameter along with the parameter name. A comma separates each parameter in the list.

Behaviorally, parameters are virtually identical to local variables, and the naming convention of parameters follows accordingly. Therefore, parameter names are camel case. Also, it is not possible to declare a local variable (a variable declared inside a method) with the same name as a parameter of the containing method, because this would create two “local variables” of the same name.

## Method Return Declaration

In addition to `GetUserInput()` and `GetFullName()` requiring parameters to be specified, both of these methods also include a **method return**. You can tell there is a method return because a data type appears immediately before the method name of the method declaration. For both `GetUserInput()` and `GetFullName()`, the data type is `string`. Unlike parameters, only one method return is allowable.

Once a method includes a return data type, and assuming no error occurs, it is necessary to specify a return statement for each **code path** (or set of statements that may execute consecutively) within the method declaration. A return statement begins with the return keyword followed by the value the method is returning. For example, the `GetFullName()` method’s return statement is `return firstName + " " + lastName`. The C# compiler makes it imperative that the return type match the type of the data specified following the return keyword.

Return statements can appear in spots other than at the end of a method implementation, as long as all code paths include a return if the method has a return type. For example, an `if` or `switch` statement at the beginning of a method implementation could include a return statement within the conditional or case statement; see Listing 4.5 for an example.

## LISTING 4.5: A Return Statement before the End of a Method

```
class Program
{
    static void Main()
    {
        string command;
        // ...
        switch(Command)
        {
            case "quit":
                return; // ...
        } // ...
    }
}
```

A return statement indicates a jump to the end of the method, so no break is required in a switch statement. Once the execution encounters a return, the method call will end.

If particular code paths include statements following the return, the compiler will issue a warning that indicates that the additional statements will never execute. In spite of the C# allowance for early returns, code is generally more readable and easier to maintain if there is a single exit location rather than multiple returns sprinkled through various code paths of the method.

Specifying void as a return type indicates that there is no return from the method. As a result, the method does not support assignment to a variable or use as a parameter type at the call site. Furthermore, the return statement becomes optional, and when it is specified, there is no value following the return keyword. For example, the return of Main() in Listing 4.4 is void and there is no return statement within the method. However, DisplayGreeting() includes a return statement that is not followed by any returned result.

## Language Contrast: C++ — Header Files

Unlike C++, C# classes never separate the implementation from the declaration. In C# there is no header (.h) file or implementation (.cpp) file. Instead, declaration and implementation appear together in the same file. Starting with C# 2.0, it is possible to spread a class across multiple files known as partial types. However, even then the declaration of a method and the implementation of that method must remain together. For C# to declare types and methods inline makes a cleaner and more maintainable language.

## BEGINNER TOPIC

## Namespaces

Namespaces are an organizational mechanism for all types. They provide a nested grouping mechanism so that types may be categorized. Developers will discover related types by examining other types within the same namespace as the initial type. Additionally, through namespaces, two or more types may have the same name as long as they are disambiguated by different namespaces.

## The using Directive

It is possible to import types from one namespace into the parent namespace code block or the entire file if there is no parent code block. As a result, it would not be necessary for the programmer to fully qualify a type. To achieve this, the C# programmer includes a using directive, generally at the top of the file. For example, in Listing 4.6, Console is not prefixed with System. Instead, it includes the using directive, using System, at the top of the listing.

## LISTING 4.6: using Directive Example

```
// The using directive imports all types from the
// specified namespace into the entire file.
using System;

class HelloWorld
{
    static void Main()
    {
        // No need to qualify Console with System
        // because of the using directive above.
        Console.WriteLine("Hello, my name is Inigo Montoya");
    }
}
```

The results of Listing 4.6 appear in Output 4.2.

## OUTPUT 4.2:

```
Hello, my name is Inigo Montoya
```

Namespaces are nested. That means that a using directive such as using System does not enable the omission of System from a method within a more specific namespace. If code accessed a type within the System.Text namespace, for example, you would have to either include an additional using directive for System.Text, or fully qualify the type. The using directive does not import any nested namespaces. Nested namespaces, identified by the period in the namespace, need to be imported explicitly.

## Language Contrast: Java—Wildcards in import Directive

Java allows for importing namespaces using a wildcard such as:

```
import javax.swing.*;
```

In contrast, C# does not support a wildcard using directive, and instead requires each namespace to be imported explicitly.

## Language Contrast: Visual Basic .NET—Project Scope Imports Directive

Unlike C#, Visual Basic .NET supports the ability to specify the using directive equivalent. Imports, for an entire project, rather than just for a specific file. In other words, Visual Basic .NET provides a command-line means of the using directive that will span an entire compilation.

Typically, prevalent use of types within a particular namespace results in a using directive for that namespace, instead of fully qualifying all types within the namespace. Following this tendency, virtually all files include the using System directive at the top. Throughout the remainder of this book, code listings will often omit the using System directive. Other namespace directives will be included explicitly, however.

One interesting effect of the using System directive is that the string data type can be identified with varying case: String or string. The former version relies on the using System directive and the latter uses the string keyword. Both are valid C# references to the System.String data type, and the resultant CIL code is unaffected by which version is chosen.²

## ADVANCED TOPIC

## Nested using Declaratives

Not only can you have using declaratives at the top of a file, but you also can include them at the top of a namespace declaration. For example, if a new namespace, Awl.Michaelis.EssentialCSharp, were declared, it would be possible to add a using declarative at the top of the namespace declaration (see Listing 4.7).

## LISTING 4.7: Specifying the using Directive inside a Namespace Declaration

```
namespace Awl.Michaelis.EssentialCSharp
{
    using System;

    class HelloWorld
    {
        static void Main()
        {
            // No need to qualify Console with System
            // because of the using directive above.
            Console.WriteLine("Hello, my name is Inigo Montoya");
        }
    }
}
```

The results of Listing 4.7 appear in Output 4.3.

## OUTPUT 4.3:

```
Hello, my name is Inigo Montoya
```

The difference between placing the using declarative at the top of a file rather than at the top of a namespace declaration is that the declarative is

2. I prefer the string keyword, but whichever representation a programmer selects, ideally code within a project should be consistent.
