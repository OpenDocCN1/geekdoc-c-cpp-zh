# Object Oriented Programming C#

In the case below one generic data type is specified. This is used to define the type of both parameters and the return value.

The generic data type identifier for a generic method can be any legal C# identifier, but by convention it is usually an upper case letter. "T" is used for "type".

When a generic method is defined i.e. one works with any data type it is specified when the method is used. Thus in the code below, Highest() is a generic method, the compiler can see that a 'Student' object is being passed as a parameter and thus the object being returned must also be of type 'Student'.

```
Student s1 = new Student("Student A");
Student s2 = new Student("Student B");
Student highestStudent = Highest(s1, s2);
```

The object being returned is of type 'Student' it must be OK to store this in a variable of type Student and it must be OK to invoke and Student methods on the object returned.

Generic methods can therefore work with any data type but the compiler can still check for type errors (as the type is specified each time the method is invoked).

Generic classes have been created, based on the same mechanisms as generic methods and these are particularly useful there were used by the creators of the .NET libraries to create generic collections.

When we won't be making much of generic methods and generic classes ourselves in this book we will be making significant use of generic collections, but before using these we need a basic understanding of collections them.

# 7.2 An Introduction to Collections

Most systems need to store various groups of entities rather than just individual items. Arrays provide one of doing this, but in C# collections are much more varied and flexible of grouping.

In C# collections classes which serve to hold together groups of objects. The .NET libraries provide several important classes defined in the System.Collections namespace that provide several different type of collection and associated functionality. This work has been developed and significantly improved upon by the creation of generic collections as defined in the System.Collections.Generic namespace. As use of non-generic collections is normally discouraged and this book will focus entirely on generic collections.