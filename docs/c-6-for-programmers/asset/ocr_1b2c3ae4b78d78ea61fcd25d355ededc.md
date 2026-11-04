**Software Engineering Observation 8.3**
*When a method receives a reference-type parameter by value, a copy of the object's reference is passed. This prevents a method from overwriting references passed to that method. In the vast majority of cases, protecting the caller's reference from modification is the desired behavior. If you encounter a situation where you truly want the called procedure to modify the caller's reference, pass the reference-type parameter using keyword ref—but, again, such situations are rare.*

**Software Engineering Observation 8.4**
*In C#, references to objects (including arrays) are passed to called methods. A called method—receiving a reference to an object in a caller—can interact with, and possibly change, the caller's object.*

# 8.14 Wrap-Up

This chapter began our discussion of C# data structures, using arrays to store data in and retrieve data from lists and tables of values. We declared, created and initialized arrays. We presented examples demonstrating common array manipulations. We introduced C#'s last control statement—the foreach iteration statement—which provides a concise and less error-prone notation for accessing data in arrays and other data structures.

We demonstrated implicitly typed local variables (with keyword var) for which the compiler determines variable types, based on their initializer values. We introduced the exception-handling mechanism and used it to allow a program to continue executing when it attempted to access an array element outside the array's bounds.

We used arrays to simulate shuffling and dealing playing cards. In that example, we introduced C# 6's getter-only auto-implemented properties, which define properties that can be used to get, but not set, a value. We also discussed auto-property initialization for auto-implemented properties.

We presented two versions of an instructor GradeBook case study that used arrays to maintain sets of student grades in memory and analyze student grades. Finally, we demonstrate how to define methods that receive variable-length argument lists and how to process command-line arguments passed to Main as a string array.

We continue our coverage of data structures in Chapter 9, where we discuss List, which is a dynamically resizable array-based collection. Chapter 18 presents generics, which provide the means to create general models of methods and classes that can be declared once, but used with many different data types. Chapter 19 introduces the data-structure classes provided by the .NET Framework, which use generics to allow you to specify the exact types of objects that a particular data structure will store. You should almost always use these predefined data structures instead of building your own. The .NET Framework also provides class Array, which contains utility methods for array manipulation, such as the Resize method introduced in this chapter.

In Chapter 9, we introduce Language Integrated Query (LINQ), which enables you to write expressions that can retrieve information from a wide variety of data sources, such as arrays. You'll see how to search, sort and filter data using LINQ.