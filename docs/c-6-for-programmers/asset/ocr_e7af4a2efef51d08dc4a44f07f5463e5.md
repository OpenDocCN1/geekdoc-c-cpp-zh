+   **Outline**
+   
+   - 18.1 Introduction
+   - 18.2 Motivation for Generic Methods
+   - 18.3 Generic-Method Implementation
+   - 18.4 Type Constraints
+     - 18.4.1 `IComparable<T>` Interface
+     - 18.4.2 Specifying Type Constraints
+   - 18.5 Overloading Generic Methods
+   - 18.6 Generic Classes
+   - 18.7 Wrap-Up

# 18.1 **Introduction**

In this chapter, we introduce C# generics and demonstrate how to create generic methods and a generic class.

# *object-Based Data Structure Disadvantages*

You can store any object in our data structures. One inconvenient aspect of storing object references occurs when retrieving them from a collection. An app normally needs to process specific types of objects. As a result, the object references obtained from a collection typically need to be downcast to an appropriate type to allow the app to process the objects correctly. In addition, data of value types (e.g., int and double) must be boxed to be manipulated with object references, which increases the overhead of processing such data. Most importantly, processing all data as type object limits the C# compiler’s ability to perform type checking.

# *Compile-Time Type Safety*

Though we can easily create data structures that manipulate any type of data as objects, it would be nice if we could detect type mismatches at compile time—this is known as compile-time type safety. For example, if a Stack should store only int values, attempting to push a string onto that Stack should cause a compile-time error. Similarly, a Sort method should be able to compare elements that are all guaranteed to have the same type. If we create type-specific versions of class Stack and method Sort, the C# compiler would certainly be able to ensure compile-time type safety. However, this would require that we create many copies of the same basic code.

# *Generics*

This chapter discusses generics, which provide the means to create the general models mentioned above. Generic methods enable you to specify, with a *single method declaration*, *a set of related methods*. Generic classes enable you to specify, with a *single class declaration*, *a set of related classes*. Similarly, generic interfaces enable you to specify, with a *single interface declaration*, *a set of related interfaces*. Generics provide *compile-time type safety*. [*Note:* You also can implement generic structs and delegates.] So far in this book, we’ve used the generic types List (Chapter 9) and Dictionary (Chapter 17).

We can write a generic method for sorting an array, then invoke the generic method separately with an int array, a double array, a string array and so on, to sort each different type of array. The compiler performs type checking to ensure that the array passed to the sorting method contains only elements of the correct type. We can write a single