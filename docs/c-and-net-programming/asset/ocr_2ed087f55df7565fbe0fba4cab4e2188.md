# ### 9.1.4 Visibility Modifiers in C#

# **Concept**

Visibility control is a key issue in object-oriented programming. Visibility-control is important because it protects the invisible parts of a class from being directly accessed from other classes. No other parts of the program can rely directly on details, which they cannot access. If some detail (typically a variable) of a class cannot be seen outside the class, it is much easier to modify this detail at a later point in time.

# **Explanation**

# **Visibility of types in assemblies and visibility of members in types**

- Visibility of a type (for example, a class) in an assembly.
  - **internal:** The type is not visible from outside the assembly.
  - **public:** The type is visible outside the assembly.
- Visibility of members in type (for example, methods in classes).
  - **private:** Accessible only in the containing type.
  - **protected:** Accessible in the containing type and in subtypes.
  - **internal:** Accessible in the assembly.
  - **protected internal:** Accessible in the assembly and in the containing type and its subtypes.
  - **public:** Accessible whenever the enclosing type is accessible.

# ### 9.1.5 Class Modifiers

# **Concept**

+   1. While implementing inheritance, it is important to understand how to establish accessibility level for newly designed derived classes and their members.

# **Explanation**

+   2. Class modifier is used to decide which parts of the system can create class objects.
+   
+      There are four different-optional-class modifiers which are,
+   
+      1. **public** - The 'public' keyword identifies a type as fully accessible to all other types. This is the implicit accessibility of enumeration members and interface members.
+   
+      2. **internal** - If a class is declared as 'internal', the type defines is accessible only to types within the same assembly (a self-contained unit of packaging' containing code, metadata etc.). This is the default access level of non-nested classes.