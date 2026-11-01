
```
credentials.Password = "password";
credentials.Domain = "explorer";

var dsmlConnection = new DsmlSoapHttpConnection(identifier, credentials);
code snippet DsmlSample/Program.cs
```

After the connection is defined, the search request can be configured. The search request consists of the directory entry where the search should start, an LDAP search filter, and the definition of what property values should be returned from the search. Here, the filter is set to (objectClass=user), so that all user objects are returned from the search. attributesToReturn is set to null, and you can read all attributes that have values. SearchScope is an enumeration in the namespace System.DirectoryServices.Protocols that is similar to the SearchScope enumeration in the namespace System.DirectoryServices used to define how deep the search should go. Here, the SearchScope is set to Subtree to walk through the complete Active Directory tree.

The search filter can be defined with an LDAP string or by using an XML document contained in the XmlDocument class:

```
string distinguishedName = null;
string ldapFilter = "(objectClass=user)";
string[] attributesToReturn = null;// return all attributes

var searchRequest = new SearchRequest(distinguishedName,
ldapFilter, SearchScope.Subtree, attributesToReturn);
```

After the search is defined with the SearchRequest object, the search is sent to the Web service by calling the method SendRequest. SendRequest is a method of the DsmlSoapHttpConnection class. SendRequest returns a SearchResponse object where the returned objects can be read.

As an alternative to invoking the synchronous SendRequest method, the DsmlSoapHttpConnection class also offers the asynchronous methods BeginSendRequest and EndSendRequest, which conform to the asynchronous .NET pattern.

![](img/d7d2ffa0a76feaab821930e95daace93_1691_0.png)

```
SearchResponse searchResponse =
(SearchResponse)dsmlConnection.SendRequest(searchRequest);
```

The returned Active Directory objects can be read within the SearchResponse. SearchResponse.Entries contains a collection of all entries that are wrapped with the type SearchResultEntry. The SearchResultEntry class has the Attributes property that contains all attributes. Each attribute can be read with help of the DirectoryAttribute class.

In the code example, the distinguished name of each object is written to the console. Next, the attribute values for the organizational unit (OU) are accessed, and the name of the organizational unit is written to the console. After this, all values of the DirectoryAttribute objects are written to the console:

```
Console.WriteLine("\r\nSearch matched {0} entries:", searchResponse.Entries.Count);
foreach (SearchResultEntry entry in searchResponse.Entries)
{
    Console.WriteLine(entry.DistinguishedName);
    // retrieve a specific attribute
    DirectoryAttribute attribute = entry.Attributes["ou"];
    Console.WriteLine("({0} = {1})", attribute.Name, attribute[0]);
```

## 53

## C#, Visual Basic, C++/CLI, and F#

## WHAT'S IN THIS CHAPTER?

- Namespaces
- Defining types
- Methods
- Arrays
- Control statements
- Loops
- Exception handling
- Inheritance
- Resource management
- Delegates
- Events
- Generics
- LINQ queries
- C++/CLI mixing native and managed code

C# is the programming language designed for .NET. More than 50 languages exist for writing .NET applications — for example, Eiffel, Smalltalk, COBOL, Haskell, Pizza, Pascal, Delphi, Oberon, Prolog, and Ruby. Microsoft alone delivers the languages C#, Visual Basic, C++/CLI, F#, JScript.NET, and F#.

Every language has advantages and disadvantages; some things can be done easily with one language but are complicated with another one. The classes from the .NET Framework are always the same, but the syntax of the language abstracts various features from the framework. For example, the C# using statement makes it easy to use the objects implementing the IDisposable interface. Other languages need more code for the same functionality.

The most commonly used .NET languages from Microsoft are C# and Visual Basic. C# was newly designed for .NET with ideas from C++, Java, Pascal, and other languages. Visual Basic has its roots in Visual Basic 6 and was extended with object-oriented features for .NET.

C++/CLI is an extension to C++ that is an ECMA standard (ECMA 372). The big advantage of C++/CLI is the ability to mix native code with managed code. You can extend existing native C++ applications and add .NET functionality, and you can add .NET classes to native libraries so that they can be used from other .NET languages such as C#. It is also possible to write completely managed applications with C++/CLI.

F# is a new language within Visual Studio that offers special support for functional programming. It works well with .NET because it supports traditional object-oriented programming as well. To give you some information what functional programming with F# means: Functions can be used as values. This makes it easy to compose functions from multiple functions, and do function pipelining where functions are chained after each other.

This chapter shows you how to convert .NET applications from one language to another. If you see sample code with Visual Basic or C++/CLI, you can easily map this to C#, and the other way around. Don't assume you can learn F# or C++/CLI with this comparison because it mainly gives information about how the C# ideas map to the other languages, but not to the core concepts and ideas of the other languages.

![](img/d7d2ffa0a76feaab821930e95daace93_1695_0.png)

## NAMESPACES

.NET types are organized into namespaces. The syntax for defining and using namespaces is quite different between the four languages:

To import namespaces, C# uses the using keyword. C++/CLI is fully based on the C++ syntax with the using namespace statement. Visual Basic defines the Imports keyword, F# defines the open keyword, to import namespaces.

With C# and Visual Basic, you can define an alias to classes or other namespaces. With C++/CLI, an alias can reference other namespaces, but not classes. C++/CLI requires the namespace keyword to define an alias — the same keyword is used to define a namespace. Visual Basic uses the Imports keyword again.

For defining namespaces, all four languages use the namespace keyword, but there's still a difference. With C++/CLI, you can't define hierarchical namespaces with one namespace statement; instead the namespaces must be nested. There's one important difference with the project settings: defining a namespace in the project settings of C# defines a default namespace that shows up in the code of all new items that you add to the project. With Visual Basic project settings, you define the root namespace that is used by all items in the project. Namespaces declared in the source code define only the sub-namespace inside the root namespace:

```
// C#
using System;
using System.Collections.Generic;
using Asm = Wrox.ProCSharp.Assemblies;
namespace Wrox.ProCSharp.Languages
{
}

// C++/CLI
using namespace System;
using namespace System::Collections::Generic;
namespace Asm = Wrox::ProCSharp::Assemblies;
namespace Wrox
{
    namespace ProCSharp
    {
        namespace Languages
```

it is also possible to declare a variable locally, but for reference types, the object is still allocated on the managed heap. With Visual Basic, the variable declaration starts with the statement Dim followed by the name of the variable. With new and the object type, memory is allocated on the managed heap:

```
// C#
MyClass obj = new MyClass();
var obj2 = new MyClass()
```

```
// C++/CLI
MyClass^ obj = gcnew MyClass();
MyClass* obj2;
```

```
' Visual Basic
Dim obj as New MyClass2()
```

If a reference type does not reference memory, different keywords are used: C# defines the null literal, C++/CLI defines nullptr (NULL is valid only for native objects), and Visual Basic defines Nothing. With F#, the null value is not normally used — it's not a value permitted with types that are defined with F#. By using types defined by languages other than F#, you might get null values.

Predefined reference types are listed in the following table. C++/CLI does not define the object and string type as is done with the other languages. Of course, you can use the classes defined by the framework.

| .NET TYPE | C# | C++/CLI | VISUAL BASIC | F# |
|---|---|---|---|---|
| System.Object | object | Not defined | Object | obj |
| System.String | string | Not defined | String | string |

## Value Types

To declare a value type, C# uses the struct keyword; C++/CLI uses the keyword value; Visual Basic, Structure, and F#, use the type keyword with the attribute [<Struct>]. An alternative is to use the struct and end keywords:

```
// C#
public struct MyStruct
{
}

// C++/CLI
public value class MyStruct
{
};

' Visual Basic
Public Structure MyStruct
End Structure

// F#
[<Struct>]
type MyStruct =
  val x : int

type MyStruct2 =
  struct
    val x : int
  end
```

With C++/CLI, you can allocate a value type on the stack, on the native heap by using the new operator, and on the managed heap by using the gcnew operator. C# and Visual Basic do not have these options, but they become important when native and managed code is mixed with C++/CLI:
