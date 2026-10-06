
# Module, Namespace, and Program Entry Points

Now that the small F# program is clean, you might want to build an executable. Listing 1-1 is a code snippet, and you will need to use Visual Studio to write, debug, and publish a product. This section will cover how to create an F# console application using Visual Studio. Figure 1-16 shows how to create an F# console application.

![](img/63aaf94e22830ab98ce16c5946be8ef6_81_0.png)

**Figure 1-16** Creating an F# console application

The default Program.fs file contains a main function with an EntryPoint attribute; see Figure 1-17. Actually, F# does not need an entry point to be defined. For a single project, the content is executed from the first line to the last.

```
// Learn more about F# at http://fsharp.net
// See the 'F# Tutorial' project for more help.

[EntryPoint]
let main argv =
    printf "%s" argv
    0 // return an integer exit code
```

**FIGURE 1-17** The default main function for an F# console application

If using the EntryPoint attribute the preferred way, the function must meet the following criteria:

- The function must be decorated with the [<EntryPoint>] attribute.
- The function must be in the last file in the project.
- The function must return an integer as exit code.
- The function must return a string array, string[], as input.

> Tip In F# DLL, modules are initialized by a static constructor. This guarantees the initialization occurs before any of the module's values are referenced. On the other hand, in an F# executable, the initialization is performed in the application's entry point, which is defined by the EntryPoint attribute. It is recommended that you explicitly define an entry point for an F# executable by using EntryPoint.

When you add the F# item in your console project, it can immediately make your code unable to compile. The newly added item is the last item in the project system. The second requirement in proceeding the list. You can use the context menu—see Figure 1-18—or Alt+Up/Down Arrow keys, if the development profile is set to F#, to move your item and down the project system.

![](img/63aaf94e22830ab98ce16c5946be8ef6_82_0.png)

**Figure 1-18** The context menu for moving an item up and down

It's always a good coding practice to divide the code into different units when the project has multiple files. F# provides the module or namespace to divide the code into small units. They have subtle differences, which I will discuss later in this chapter.

If you delete all content in the Program.fs file and paste the code shown in Listing 1-33, which does not have a module definition, the F# compiler will create an anonymous module. Its name is the name with the first letter capitalized. For example, if your code is in file1.fs, the module name will be File1. You can also explicitly provide module names at the first line of the file, as shown in Listing 1-88.

**LISTING 1-88** Module definition

```
module MyModule

printf "Hello World"
```

A module can contain other modules, type definitions, expressions, values, or any combination of those, but namespaces cannot be inside a module. The nested module needs to be indented and have have an equal sign (=) as a suffix. See Listing 1-89.

# LISTING 1-89 Defining a nested module

```
module Print

// general print function
let x = printf("%A") x

// define sub module NumberPrint
module NumberPrint =
  // function to print int
  let printInt = printf("%d")

  // function to print float
  let printFloat = printf("%f")

// define sub module StringPrint
module StringPrint =
  // function to print string
  let printString = printf("%s")

  // function to print char
  let printChar = printf("%c")

// define sub module with new type
module NewTypes =
  // define a 2D point
  type Point2D = float32*float32

// invoke print functions
NumberPrint.printFloat 4.5
NumberPrint.printInt 2
StringPrint.printChar 'c'
StringPrint.printString "abc"
```

If you want to hold the functions and variables, the namespace and module are the same from F#'s point of view. If the F# project is to be a library opened from a C# project, the namespace is a better choice. The module is a static class when it's viewed from the C# side. By using a module name and function name together, you can reference a function defined in a different module. If you want to reference a function inside a module, you can use the open keyword to open that module or decorate the module with the AutoOpen attribute, which can open the module automatically, essentially causing the function to be placed in the global namespace. See Listing 1-90.

```
module Print
// general print function
let print x = printf("%A") x

// auto open NumberPrint
[-AutoOpen]
module NumberPrint =
    // function to print int
    let printInt = printf("%d")

    // function to print float
    let printFloat = printf("%f")

module StringPrint =
    // function to print string
    let printString = printf("%s")

    // function to print char
    let printChar = printf("%c")

// invoke print functions
printFloat 4.5
printInt 2

// use module name to reference the function defined in the module
StringPrint.printChar 'c'
StringPrint.printString "abc"

// open StringPrint module
open StringPrint
printChar 'c'
printString "abc"
```

> Note The open statement must be located somewhere after the module is defined.

The RequireQualifiedAccess attribute indicates that a reference to an element in that module must specify the module name. Listing 1-91 shows how to decorate the attribute on a module and reference a function within.

# LISTING 1-91 Using the RequireQualifiedAccess attribute

```
[<RequireQualifiedAccessAttribute>
module MyModule =
 let f() = printf %f inside MyModule

//reference to f must use MyModule
MyModule.f()
```

Modules can be extended by creating a new module with the same name. All the items—such as functions, types, expressions, values—will be accessible as long as the new module is. Listing 1-92 shows. To invoke the method, you can open the namespace. Listing 1-92 shows, and usually with less code.

> 92 Extending a module

```
namespace CollectionExtensions

open System.Generic

// extend the method
module Array =
 let lengthBy (fun n -> n % 2 = 0)
```

> Note A module inside a namespace needs equal sign (=) as a suffix.

As mentioned previously, if F# code needs to be referenced from other languages, a namespace is the preferred way. Namespaces can contain only modules and type definitions. Listing 1-94.

# LISTING 1-94 Using a namespace

```
namespace Space

// define a 3D point
type Point3D = Point of float32 * float32 * float32

// define module inside namespace
module HelloWorld =
  let msg = "%Hello"

// the following line won't compile because a namespace contain value or expression
// let a = 2
```

> Note Namespaces are not supported in FSI because it's difficult to find out where the namespace ends.

Empty files do not compile in a multif project. Source code must have either a namespace or a module at the beginning if the project contains multiple files.

![](img/63aaf94e22830ab98ce16c5946be8ef6_86_0.png)

# Using F# for Object-Oriented Programming

Object-oriented programming (OOP) has been a great success. Many modern business systems are designed and implemented by applying OOP concepts. I will not discuss the benefit of OOP as a C# developer, you probably have hundreds of such benefits in mind.

F# is a multiparadigm language that supports OOP. Practically everything you can do with C# can be done with F#, and usually with less code. I will follow the approach from the first chapter, converting C# code to F#: Listing 2-1 shows a C# Point2D class, which represents a point on a twodimensional (2D) surface. It shows properties, static and nonstatic fields, an attribute, and member methods. The conversion will not only do the straightforward translation, but also perform some extra work to demonstrate related F# concepts.

ING 2-1 C# Point2D class definition

```
// define a 2D point
[Debugger("{X}, {Y}")]
public class Point2D
{
    // define a counter
    private static int count = 0;
    // define the original point
    public readonly Point2D OriginalPoint = new Point2D(0, 0);

    // define an X property with explicit back-end field
    private double x;
    public double X
    {
        get { return this.x; }
        set { this.x = value; }
    }

    // define a Y property
    public double Y { get; set; }
}
```
