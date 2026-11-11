# ## 11.4.4 Abstract Data Types in C#

Recall that C# is based on both C++ and Java and that it also includes some new constructs. Like Java, all C# class instances are heap dynamic. Default constructors, which provide initial values for instance data, are predefined for all classes. These constructors provide typical initial values, such as 0 for **int** types and **false** for **boolean** types. A user can furnish one or more constructors for any class he or she defines. Such constructors can assign initial values to some or all of the instance data of the class. Any instance variable that is not initialized in a user-defined constructor is assigned a value by the default constructor.

Although C# allows destructors to be defined, because it uses garbage collection for most of its heap objects, destructors are rarely used.

# ### 11.4.4.1 Encapsulation

As mentioned in Section 11.4.2, C++ includes both classes and structs, which are nearly identical constructs. The only difference is that the default access modifier for class is **private**, whereas for structs it is **public**. C# also has structs, but they are very different from those of C++. In C#, structs are, in a sense, lightweight classes. They can have constructors, properties, methods, and data fields and can implement interfaces but do not support inheritance. One other important difference between structs and classes in C# is that structs are value types, as opposed to reference types. They are allocated on the run-time stack, rather than the heap. If they are passed as parameters, like other value types, by default they are passed by value. All C# value types, including all of its primitive types, are actually structs. Structs can be created by declaring them, like other predefined value types, such as **int** or **float**. They can also be created with the **new** operator, which calls a constructor to initialize them.

Structs are used in C# primarily to implement relatively small simple types that need never be base types for inheritance. They are also used when it is convenient for the objects of the type to be stack as opposed to heap allocated.

# ### 11.4.4.2 Information Hiding

C# uses the **private** and **protected** access modifiers exactly as they are used in Java.

C# provides properties, which it inherited from Delphi, as a way of implementing getters and setters without requiring explicit method calls by the client. As with Objective-C, properties provide implicit access to specific **private** instance data. For example, consider the following simple class and client code:

```
    public class Weather {
        public int DegreeDays {  // DegreeDays is a property
            get {
                return degreeDays;
            }
        }
    }
```