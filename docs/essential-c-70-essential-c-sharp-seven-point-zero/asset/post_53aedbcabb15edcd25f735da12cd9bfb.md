
and have appropriate permissions granted. Programs run from a remote location will need to be explicitly granted such a right.

![](img/ef6a8a417630b222bfb3f3b949facff0_766_0.png)

**FIGURE 18.1: MemberInfo Derived Classes**

![](img/ef6a8a417630b222bfb3f3b949facff0_767_0.png)

## Reflection on Generic Types

The introduction of generic types in version 2.0 of the Common Language Runtime (CLR) necessitated additional reflection features. Runtime reflection on generics determines whether a class or method contains a generic type and any type parameters or arguments it may include.

### Determining the Type of Type Parameters

In the same way that you can use a *typeof* operator with nongeneric types to retrieve an instance of `System.Type`, so you can use the *typeof* operator on type parameters in a generic type or generic method. Listing 18.4 applies the *typeof* operator to the type parameter in the *Add* method of a *Stack* class.

**LISTING 18.4: Declaring the Stack<> Class**

```
public class Stack<T>
{
 // ...
 public void Add(T i)
 {
 // ...
 Type t = typeof(T);
 // ...
 }
 // ...
}
```

Once you have an instance of the *Type* object for the type parameter, you may then use reflection on the type parameter itself to determine its behavior and tailor the *Add* method to the specific type more effectively.

### Determining Whether a Class or Method Supports Generics

In the `System.Type` class for the version 2.0 release of the CLR, a handful of methods were added that determine whether a given type supports generic parameters and arguments. A generic argument is a type parameter supplied when a generic class is instantiated. You can determine whether a class or method contains generic parameters that have not yet been set by querying the `Type.ContainsGenericParameters` property, as demonstrated in Listing 18.5.

**LISTING 18.5: Reflection with Generics**

```csharp
using System;

public class Program
{
    static void Main()
    {
        Type type;
        type = typeof(System.Nullable<>);
        Console.WriteLine(type.ContainsGenericParameters);
        Console.WriteLine(type.IsGenericType);

        type = typeof(System.Nullable<DateTime>);
        Console.WriteLine(!type.ContainsGenericParameters);
        Console.WriteLine(type.IsGenericType);
    }
}
```

Output 18.3 shows the results of Listing 18.5.

**OUTPUT 18.3**

```
True
True
True
True
```

Type.IsGenericType is a Boolean property that evaluates whether a type is generic.

### Obtaining Type Parameters for a Generic Class or Method

You can obtain a list of generic arguments, or type parameters, from a generic class by calling the GetGenericArguments( ) method. The result is an array of System.Type instances that corresponds to the order in which they are declared as type parameters of the generic class. Listing 18.6 reflects into a generic type and obtains each type parameter; Output 18.4 shows the results.

**LISTING 18.6: Using Reflection with Generic Types**

```csharp
using System;
using System.Collections.Generic;

public partial class Program
{
    public static void Main()
    {
        Stack<int> s = new Stack<int>();

        Type t = s.GetType();

        foreach (Type type in t.GetGenericArguments())
        {
            System.Console.WriteLine(
                "Type parameter: " + type.FullName);
        } // ...
    }
}
```

**OUTPUT 18.4**

```
Type parameter: System.Int32
```

## nameof Operator

We briefly touched on the nameof operator in Chapter 11, where it was used to provide the name of a parameter in an argument exception:

```
throw new ArgumentException(
    "The argument did not represent a digit", nameof(textDigit));
```

Introduced in C# 6.0, this contextual keyword produces a constant string containing the unqualified name of whatever program element is specified as an argument. In this case, textDigit is a parameter to the method, so nameof(textDigit) returns “textDigit.” (Given that this activity happens at compile time, nameof is not technically reflection. We include it here because ultimately it receives data about the assembly and its structure.)

You might ask what advantage is gained by using nameof(textDigit) over simply "textDigit" (especially given that the latter might even seem easier to use to some programmers). The advantages are twofold:

- The C# compiler ensures that the argument to the nameof operator is, in fact, a valid program element. This helps prevent errors when a program element name is changed, helps prevent misspellings, and so on.
- IDE tools work better with the nameof operator than with literal strings. For example, the “find all references” tool will find program elements mentioned in a nameof expression but not in a literal string. The automatic renaming refactoring also works better, and so on.

In the snippet given earlier, nameof(textDigit) produces the name of a parameter. However, the nameof operator works with any program element. For example, Listing 18.7 uses nameof to pass the property name to INotifyPropertyChanged.PropertyChanged.

**LISTING 18.7: Dynamically Invoking a Member**

```csharp
using System.ComponentModel;

public class Person : INotifyPropertyChanged
{
    public event PropertyChangedEventHandler PropertyChanged;
    public Person(string name)
    {
        Name = name;
    }
    private string _Name;
    public string Name
    {
        get { return _Name; }
        set
        {
            if (_Name != value)
            {
                _Name = value;
                // Using C# 6.0 conditional null reference
                PropertyChanged?.Invoke(
                    this,
                    new PropertyChangedEventArgs(
                        nameof(Name)));
            }
        }
    }
    // ...
}
```

Notice that whether only the unqualified “Name” is provided (because it’s in scope) or the fully (or partially) qualified name such as Person.Name is used, the result is only the final identifier (the last element in a dotted name). You can still use C# 5.0's CallerMemberName parameter attribute to obtain a property's name; see http://itl.tc/CallerMemberName for an example.

## Attributes

Before delving into details on how to program attributes, we should consider a use case that demonstrates their utility. In the `CommandLineHandler` example in Listing 18.3, you dynamically set a class’s properties based on the command-line option matching the property name. This approach is insufficient, however, when the command-line option is an invalid property name. `/?,` for example, cannot be supported. Furthermore, this mechanism doesn’t provide any way of identifying which options are required versus which are optional.

Instead of relying on an exact match between the option name and the property name, you can use attributes to identify additional metadata about the decorated construct—in this case, the option that the attribute decorates. With attributes, you can decorate a property as `Required` and provide a `/ ?` option alias. In other words, attributes are a means of associating additional data with a property (and other constructs).

Attributes appear within square brackets preceding the construct they decorate. For example, you can modify the `CommandLineInfo` class to include attributes, as shown in Listing 18.8.

**LISTING 18.8: Decorating a Property with an Attribute**

```csharp
class CommandLineInfo
{
    [CommandLineSwitchAlias("?")]
    public bool Help { get; set; }
    [CommandLineSwitchRequired]
    public string Out { get; set; }
    public System.Diagnostics.ProcessPriorityClass Priority { get; set; } =
    System.Diagnostics.ProcessPriorityClass.Normal;
}
```

In Listing 18.8, the `Help` and `Out` properties are decorated with attributes. The purpose of these attributes is to allow an alias of `/?` for `/Help,` and to indicate that `/Out` is a required parameter. The idea is that from within the `CommandLineHandler.TryParse()` method, you enable support for option aliases and, assuming the parsing was successful, you check that all required switches were specified.
