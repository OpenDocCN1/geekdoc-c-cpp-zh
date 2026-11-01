# An Introduction to Generics

Since their introduction with .NET 2.0, generics pop up in many different locations in the .NET Framework. Although they are used often in situations where collections are used, the use of generics is not limited to collections; you can also use them for singular types of objects.

Generics are to code what Microsoft Word templates are to word processing. They enable you to write a code template that can be used in different scenarios with different types. With generics, you can define a generic code template that doesn't explicitly specify a type. Only when that code is used do you define the type. The main benefit of this is that you can reuse the same template over and over again for multiple data types, without retyping and maintaining multiple versions of the code. In addition to using generics in your own code definitions, you find a host of generics-enabled objects and collections in the .NET Framework, ready to be used by your code.

To understand how you can take advantage of generics, take a look at the following example. It's essentially the same code you saw earlier where the ArrayList was used, but this time the type of the list is constrained so it accepts only strings:

```
VB.NET
Dim roles As New List(Of String)

roles.Add("Administrators")
roles.Add("ContentManagers")
roles.Add("Members")
```

```
C#
List<string> roles = new List<string>();
roles.Add("Administrators");
roles.Add("ContentManagers");
roles.Add("Members");
```

Not much has changed to make the roles list type safe. However, with the definition of List(Of String) in VB.NET and List<string> in C# the new list is now set up to allow only strings to be added through its Add method. This compiles fine:

```
roles.Add("Administrators");
```

The following will not compile because 33 is not a String:

```
roles.Add(33);
```

Similar to a generics list of strings, you can also create lists to hold other types. For example:

```
VB.NET
Dim intList As New List(Of Integer)    ' Can hold Integers only
Dim boolList As New List(Of Boolean)   ' Can hold Booleans only
Dim buttonList As New List (Of Button) ' Can hold Button controls only
```

```
C#
List<int> intlist = new List<int>();    // Can hold ints only
List<bool> boollist = new List<bool>(); // Can hold bools only
List<Button> buttonlist = new List<Button>(); // Can hold Button controls only
```