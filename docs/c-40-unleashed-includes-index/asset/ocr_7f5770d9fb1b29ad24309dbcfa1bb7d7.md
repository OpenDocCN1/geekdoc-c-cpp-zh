+   - Types can be classified in various categories:
+     - IsPrimitive returns true for types considered primitive (such as int).
+     - IsArray indicates whether you are dealing with an array type.
+     - IsValueType distinguishes value types (like structs and enums).
+     - IsClass, IsInterface and IsEnum should be self-explanatory.
+     - IsCOMObject reveals the CLR's integration facilities to deal with types from the COM world.
+     - IsPointer reveals pointer types, used in unsafe code. Notice those are not the same as reference types. For more information, read up on programming with unsafe code in languages like C#.

+   - Since their introduction in .NET 2.0, generics have invaded most portions of the CLR one way or another, including the reflection subsystem:
+     - IsGenericType tells whether a type is generic (for example, List<int>).
+     - IsGenericTypeDefinition indicates generic type definitions such as List<T>, where T is not bound (the generic parameter is left "open") to a type. In C#, you can write typeof(List<>) to obtain such a type.
+     - ContainsGenericParameters will point out remaining "open" generic parameters on a type (for example, if a List<T> doesn't have its T substituted for a specific type).
+     - IsGenericParameter will be true for Type objects retrieved from calls to obtain the generic parameters on a generic type, such as the T in List<T>.
+     - GenericParameterPosition goes with the previous property, indicating the zero-based position of the generic parameter. For example, in Dictionary<K, T>, the Type object for T will have position index 1 while K will have a GenericParameterPosition of 0.
+   - Other properties are a bit more obscure, so I'll direct the interested reader to MSDN documentation on the subject.

# Discovering Types

Now that you know we can query lots of properties of types, we should briefly revisit how we can obtain the Type objects themselves. There are three main ways to do so, the first of which we've already covered: use of the typeof operator in C#. Although this way is the most direct, it has little value in scenarios where you're really about to find out about type information you didn't know about at compile time:

```
var stringType = typeof(string /* you did know the type name, didn't you? */);
var intType = typeof(int /* same story here */);
```