# Namespaces, the Preprocessor, and Assemblies

This chapter discusses three C# features that give you greater control over the organization and accessibility of a program. These are namespaces, the preprocessor, and assemblies.

# Namespaces

The namespace was mentioned briefly in Chapter 2 because it is a concept fundamental to C#. In fact, every C# program makes use of a namespace in one way or another. We didn’t need to examine namespaces in detail before now because C# automatically provides a default, global namespace for your program. Thus, the programs in earlier chapters simply used the global namespace. In the real world, however, many programs will need to create their own namespaces or interact with other namespaces. Here, they are examined in detail.

A namespace defines a declarative region that provides a way to keep one set of names separate from another. In essence, names declared in one namespace will not conflict with the same names declared in another. The namespace used by the .NET Framework library (which is the C# library) is System. This is why you have included

```
using System;
```

near the top of every program. As explained in Chapter 14, the I/O classes are defined within a namespace subordinate to System called System.IO. There are many other namespaces subordinate to System that hold other parts of the C# library.

Namespaces are important because there has been an explosion of variable, method, property, and class names over the past few years. These include library routines, third-party code, and your own code. Without namespaces, all of these names would compete for slots in the global namespace and conflicts would arise. For example, if your program defined a class called Finder, it could conflict with another class called Finder supplied by a third-party library that your program uses. Fortunately, namespaces prevent this type of problem because a namespace restricts the visibility of names declared within it.