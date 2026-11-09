
The extension method above can now be invoked using any expression that results in a type that implements the IEnumerable<T> interface:

```csharp
public static void Main() {
    // Shows each Char on a separate line in the console
    "Grant".ShowItems();

    // Shows each String on a separate line in the console
    new[] { "Jeff", "Kristin" }.ShowItems();

    // Shows each Int32 value on a separate line in the console
    new List<Int32>() { 1, 2, 3 }.ShowItems();
}
```

> **Important** Extension methods are the cornerstone of Microsoft's Language Integrated Query (LINQ) technology. For a great example of a class that offers many extension methods, see the static **System.Linq.Enumerable** class and all its static extension methods in the Microsoft .NET Framework SDK documentation. Every extension method in this class extends either the **IEnumerable** or **IEnumerable<T>** interface.

You can define extension methods for delegate types, too. For an example of this, turn to page 278 in Chapter 11, “Events.” You can also add extension methods to enumerated types. I show an example of this in the “Adding Methods to Enumerated Types” section in Chapter 15, “Enumerated Types and Bit Flags.”

And last but not least, I want to point out that the C# compiler allows you to create a delegate (see Chapter 17, “Delegates,” for more information) that refers to an extension method over an object:

```csharp
public static void Main () {
    // Create an Action delegate that refers to the static ShowItems extension method
    // and has the first argument initialized to reference the “Jeff” string.
    Action a = "Jeff".ShowItems;
    .
    .
    .
    // Invoke the delegate which calls ShowItems passing it a reference to the “Jeff” string.
    a();
}
```

In the code above, the C# compiler generates IL code to construct an **Action** delegate. When creating a delegate, the constructor is passed the method that should be called and is also passed a reference to an object that should be passed to the method's hidden **this** parameter. Normally, when you create a delegate that refers to a static method, the object reference is **null** since static methods don't have a **this** parameter. However, in this example, the C# compiler generated some special code that creates a delegate that refers to a static method (**ShowItems**) and the target object of the static method is the reference to the “Jeff” string. Later, when the delegate is invoked, the CLR will call the static method and will pass to it the reference to the “Jeff” string. This is a little hacky, but it works great and it feels natural so long as you don't think about what is happening internally.

### The Extension Attribute

It would be best if this concept of extension methods was not C#-specific. Specifically, we want programmers to define a set of extension methods in some programming language and for people in other programming languages to take advantage of them. For this to work, the compiler of choice must support searching static types and methods for potentially matching extension methods. And compilers need to do this quickly so that compilation time is kept to a minimum.

In C#, when you mark a static method's first parameter with the **this** keyword, the compiler internally applies a custom attribute to the method and this attribute is persisted in the resulting file's metadata. The attribute is defined in the System.Core.dll assembly, and it looks like this:

```csharp
// Defined in the System.Runtime.CompilerServices namespace
[AttributeUsage(AttributeTargets.Method | AttributeTargets.Class | AttributeTargets.Assembly)]
public sealed class ExtensionAttribute : Attribute {
}
```

In addition, this attribute is applied to the metadata for any static class that contains at least one extension method. And this attribute is also applied to the metadata for any assembly that contains at least one static class that contains an extension method. So now, when compiling code that invokes an instance method that doesn't exist, the compiler can quickly scan all the referenced assemblies to know which ones contain extension methods. Then it can scan only these assemblies for static classes that contain extension methods, and it can scan just the extension methods for potential matches to compile the code as quickly as possible.

![](img/3c46ff5b170881db4209d365b1f7a808_230_0.png)

> **Note** The **ExtensionAttribute** class is defined in the System.Core.dll assembly. This means that the resulting assembly produced by the compiler will have a reference to System.Core.dll embedded in it even if I do not use any types from System.Core.dll and do not even reference System.Core.dll when compiling my code. However, this is not too bad a problem because the **ExtensionAttribute** is used only at compile time; at runtime, System.Core.dll will not have to be loaded unless the application consumes something else in this assembly.

### Partial Methods

Imagine that you use a tool that produces a C# source code file containing a type definition. The tool knows that there are potential places within the code it produces where you might want to customize the type's behavior. Normally, customization would be done by having the tool-produced code invoke virtual methods. The tool-produced code would also have to contain definitions for these virtual methods, and the way these methods would be implemented is to do nothing and simply return. Now, if you want to customize the behavior of the class, you'd define your own class, derive it from the base class, and then override any virtual methods implementing it so that it has the behavior you desire. Here is an example:

```csharp
// Tool-produced code in some source code file:
internal class Base {
    private String m_name;

    // Called before changing the m_name field
    protected virtual void OnNameChanging(String value) {
    }

    public String Name {
        get { return m_name; }
        set {
            OnNameChanging(value.ToUpper());  // Inform class of potential change
            m_name = value;                   // Change the field
        }
    }
}
```

```csharp
// Developer-produced code in some other source code file:
internal class Derived : Base {
    protected override void OnNameChanging(String value) {
        if (String.IsNullOrEmpty(value))
            throw new ArgumentNullException("value");
    }
}
```

Unfortunately, there are two problems with the code above:

- The type must be a class that is not sealed. You cannot use this technique for sealed classes or for value types (because value types are implicitly sealed). In addition, you cannot use this technique for static methods since they cannot be overridden.
- There are efficiency problems here. A type is being defined just to override a method; this wastes a small amount of system resources. And, even if you do not want to override the behavior of **OnNameChanging**, the base class code still invokes a virtual method which simply does nothing but return. Also, **ToUpper** is called whether **OnNameChanging** accesses the argument passed to it or not.

C#'s partial methods feature allows you the option of overriding the behavior of a type while fixing the aforementioned problems. The code below uses partial methods to accomplish the same semantics as the previous code:

A partial method cannot have an **out** parameter because the method would have to initialize it and the method might not exist. A partial method may have **ref** parameters, may be generic, may be instance or static, and may be marked as **unsafe**.

- Of course, the defining partial method declaration and the implementing partial method declaration must have identical signatures. If both have custom attributes applied to them, then the compiler combines both methods' attributes together. Any attributes applied to a parameter are also combined.
- If there is no implementing partial method declaration, then you cannot have any code that attempts to create a delegate that refers to the partial method. Again, the reason is that the method doesn't exist at runtime. The compiler produces this message: **"error CS0762: Cannot create delegate from method 'Base.OnNameChanging(string)' because it is a partial method without an implementing declaration"**.
- Partial methods are always considered to be private methods. However, the C# compiler forbids you from putting the **private** keyword before the partial method declaration.
