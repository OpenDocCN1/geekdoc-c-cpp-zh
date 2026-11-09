# # Type and Member Basics

In this chapter:

+   - The Different Kinds of Type Members ...... 151
+   - Type Visibility ...... 154
+   - Member Accessibility ...... 156
+   - Static Classes ...... 158
+   - Partial Classes, Structures, and Interfaces ...... 159
+   - Components, Polymorphism, and Versioning ...... 160

In Chapters 4 and 5, I focused on types and what operations are guaranteed to exist on all instances of any type. I also explained how all types fall into one of two categories: reference types and value types. In this and the subsequent chapters in this part, I'll show how to design types by using the different kinds of members that can be defined within a type. In Chapters 7 through 11, I'll discuss the various members in detail.

# ## The Different Kinds of Type Members

A type can define zero or more of the following kinds of members:

+   - **Constants** A constant is a symbol that identifies a never-changing data value. These symbols are typically used to make code more readable and maintainable. Constants are always associated with a type, not an instance of a type. Logically, constants are always static members. Discussed in Chapter 7, "Constants and Fields."
+   - **Fields** A field represents a read-only or read/write data value. A field can be static, in which case the field is considered part of the type's state. A field can also be instance (nonstatic), in which case it's considered part of an object's state. I strongly encourage you to make fields private so that the state of the type or object can't be corrupted by code outside of the defining type. Discussed in Chapter 7.
+   - **Instance constructors** An instance constructor is a special method used to initialize a new object's instance fields to a good initial state. Discussed in Chapter 8.
+   - **Type constructors** A type constructor is a special method used to initialize a type's static fields to a good initial state. Discussed in Chapter 8.