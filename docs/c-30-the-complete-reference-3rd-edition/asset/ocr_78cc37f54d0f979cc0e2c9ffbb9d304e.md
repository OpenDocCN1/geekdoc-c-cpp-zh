In general, a new executable version of a generic class is created for each constructed type in which the type argument is a value type, such as int or double. Thus, each object of Gen<int> will use one version of Gen and each object of type Gen<double> will use another version of Gen, with each version of Gen tailored to the specific value type. However, there will be only one version of a generic class that handles all cases in which the type argument is a reference type. This is because the size (in bytes) of all references is the same. Thus, only one version is needed to handle all types of references. This optimization also reduces code-bloat.

# Some Generic Restrictions

Here are a few restrictions that you need to keep in mind when using generics:

+   - Properties, operators, indexers, and events cannot be generic. However, these items can be used in a generic class and can make use of the generic type parameters of that class.
+   - The extern modifier cannot be applied to a generic method.
+   - Pointer types cannot be used as type arguments.
+   - If a generic class contains a static field, then each constructed type has its own copy of that field. This means that each instance of the same constructed type shares the same static field. However, a different constructed type shares a different copy of that field. Thus, a static field is not shared by all constructed types.

# Final Thoughts on Generics

Generics are a powerful extension to C# because they streamline the creation of type-safe, reusable code. Although the generic syntax can seem a bit overwhelming at first, it will quickly become second nature. Likewise, learning how and when to use constraints takes a bit of practice, but becomes easier over time. Generics are now an integral part of C# programming. It's worth the effort it takes to master this important feature.