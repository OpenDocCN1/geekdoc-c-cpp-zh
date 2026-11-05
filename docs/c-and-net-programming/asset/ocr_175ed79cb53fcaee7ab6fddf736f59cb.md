| int | 0 |
| object reference | Null |

Table 8.1.1 Default values of the fields

# 9. Static and instance initialization

+   1. Static fields and static properties are data members associated with the class itself, rather than with the instances of that class.
+   2. A static constructor can be used to initialize static members.
+   3. Static fields can be initialized at the time of their declaration.
+   4. The first time when a static member is referred, the following events take place,
+      1. All static fields are initialized to their respective default values.
+      2. The static constructor is called.
+      3. Code that accesses the static member is executed.

+   5. In case of reference to an instance method or during the instance creation of the class, before referencing any static members, the following events take place,
+      1. All static fields are initialized to their respective default values.
+      2. The static constructor is called.
+      3. All instance fields are initialized to their respective default values.
+      4. The instance constructor is called.
+      5. Code that accesses an instance member is executed.

# 1.3 Properties

# Concept

+   1. **Properties** are named members of classes, structures and interfaces. Property is mechanism by which field in a class is protected through specialized reading and writing method.

# Explanation

+   2. Member variables in a class or structures are called **Fields and** properties are extension of fields and are accessed using the same syntax.
+   3. Property use **accessors** through which the values of the private fields can be read, written or manipulated.
+   4. Specialized getter and setter methods are implemented for field for accessing it.