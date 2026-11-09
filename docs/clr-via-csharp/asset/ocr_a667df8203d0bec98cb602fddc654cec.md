# # Fields

A *field* is a data member that holds an instance of a value type or a reference to a reference type. Table 7-1 shows the modifiers that can be applied to a field.

**TABLE 7-1 Field Modifiers**

| CLR Term | C# Term | Description |
|---|---|---|
| Static | **static** | The field is part of the type's state, as opposed to being part of an object's state. |
| Instance | (default) | The field is associated with an instance of the type, not the type itself. |
| InitOnly | **readonly** | The field can be written to only by code contained in a constructor method. |
| Volatile | **volatile** | Code that accesses the field is not subject to some thread-unsafe optimizations that may be performed by the compiler, the CLR, or by hardware. Only the following types can be marked **volatile**: all reference types, **Single, Boolean, Byte, SByte, Int16, UInt16, Int32, UInt32, Char**, and all enumerated types with an underlying type of **Byte, SByte, Int16, UInt16, Int32, or UInt32**. Volatile fields are discussed in Chapter 28, “Primitive Thread Synchronization Constructs.” |

As Table 7-1 shows, the common language runtime (CLR) supports both static (and instance) nonstatic fields. For type fields, the dynamic memory required to hold the field's data is allocated inside the type object, which is created when the type is loaded into an AppDomain (see Chapter 22, “CLR Hosting and AppDomains”), which typically happens the first time any method that references the type is just-in-time (JIT)–compiled. For instance fields, the dynamic memory to hold the field is allocated when an instance of the type is constructed.

Because fields are stored in dynamic memory, their value can be obtained at runtime only. Fields also solve the versioning problem that exists with constants. In addition, a field can be of any data type, so you don't have to restrict yourself to your compiler's built-in primitive types (as you do for constants).

The CLR supports **readonly** fields and **read/write** fields. Most fields are **read/write** fields, meaning the field's value might change multiple times as the code executes. However, **readonly** fields can be written to only within a constructor method (which is called only once, when an object is first created). Compilers and verification ensure that **readonly** fields are not written to by any method other than a constructor. Note that reflection can be used to modify a **readonly** field.

Let’s take the example from the “Constants” section and fix the versioning problem by using a static **readonly** field. Here’s the new version of the DLL assembly’s code: