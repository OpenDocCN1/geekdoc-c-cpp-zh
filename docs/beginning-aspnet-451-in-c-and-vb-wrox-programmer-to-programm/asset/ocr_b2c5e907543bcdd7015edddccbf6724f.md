```
roles.Add("ContentManagers")   ' Add the second role
roles.Add("Members")             ' Keep adding roles and the ArrayList
                                     ' grows as necessary
```

# C#

```
ArrayList roles = new ArrayList(); // Create a new ArrayList. You don't need
                                            // to set its size explicitly

roles.Add("Administrators");      // Add the first role
roles.Add("ContentManagers")   // Add the second role
roles.Add("Members");             // Keep adding roles and the ArrayList
                                     // grows as necessary
```

Because this code now calls a method (Add) rather than assigning it to a predefined index in an array, you need parentheses (()) in both VB.NET and C#. The usage of methods is discussed later in this chapter.

All collections solve some of the problems that arrays have, introduce a few problems of others. Their biggest drawback is that it isn't strongly typed. What means is that you can add any object to the list using the Add method. This means that the ArrayList can hold objects that are different types of the same. This might not seem to be a big deal at first, but as you start working with an ArrayList that contains multiple types of objects, you'll quickly see why this is problematic. The role takes an example. With the array and ArrayList versions, the code simply added a few strings containing name. You can then use these strings, to build up a drop-down list in a Web Form to enable a user to pick a role. So far, good, but what if one of the items in the list is not a string? What if another developer accidentally wrote some code that adds a Drop control to the ArrayList? Because ArrayList accepts all objects, it won't complain. However, your code will crash if it expects a String, but get a DropList control instead.

With .NET 2.0, Microsoft introduced a concept called generics. Generics are still strongly present in version 4.5.1 of .NET, helping you overcome the problems that weakly typed collections like the ArrayList introduced.

# An Introduction to Generics

Since their introduction with .NET 2.0, generics pop up in many locations in the .NET Framework. Although they are used in situations where collections are used, the use of generics is not limited to collections; you can also use them for simpler types of objects.

Generics are to what Word templates are to word processing. They enable you to write a code template that can be used in different scenarios with different types. With generics, you can define a generic template that doesn't specify a type. Only when you do define the type. The main benefit of this is that you can reuse the same template over and again for multiple data types, without rewriting and maintaining multiple versions of the code. In addition to using generics in your code definitions, you can find a host of generics-enabled objects and collections in the .NET Framework, ready to be used by your code.

To understand how you can take advantage of generics, take a look at the following example. It's essentially the same code you saw earlier where the ArrayList was used, but this time the type of the list is constrained so it accepts only strings: