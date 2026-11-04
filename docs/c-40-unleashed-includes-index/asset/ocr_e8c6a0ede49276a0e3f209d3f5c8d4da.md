IN THE DATABASE WORLD...

Reflection might seem a little weird at first, but it's a widespread concept throughout many systems. Databases, in particular today's relational ones, have had ways to describe the structure of tables for ages. The way you get to information like this is by simply writing a query over a system table (or a management view) that exposes it. Because of this, you don't have to learn different concepts to learn about the system. Reuse of the same toolbox is a great benefit.

# Properties Describing Types

Types have many properties describing them. Let's take a look at most of them:

+   1. Visibility can be inspected through various properties, such as the following:
+      - IsPublic indicates whether the type was declared to be public.
+      - IsNonPublic is essentially the opposite of the above.
+      - IsVisible reveals whether a type can be accessed outside the assembly it's defined in. For nested types, this can differ from IsPublic.

+   2. Types have names, which can be broken up in different ways:
+      - Name is the name of the type as is was declared (for example, String).
+      - Namespace tells what namespace the type is in (for example, System).
+      - FullName combines the above, dot-separated (for example, System.String).
+      - AssemblyQualifiedName also includes the name of the assembly in which the type lives (for example, System.String, mscorlib).

+   3. To find out where types live, the following properties are handy:
+      - Assembly reveals the assembly defining the type.
+      - Module indicates the module within the type's defining assembly.
+      - DeclaringType is usable for nested types, indicating the parent type. The property IsNested is related to this in an obvious manner.

+   4. Object orientation is deeply rooted in the CLR's type system, as witnessed by the following properties:
+      - BaseType, for the type's immediate base type
+      - IsAbstract, indicating whether the type is abstract
+      - IsInterface, identifying interface types
+      - IsSealed, corresponding to the sealed keyword in C#