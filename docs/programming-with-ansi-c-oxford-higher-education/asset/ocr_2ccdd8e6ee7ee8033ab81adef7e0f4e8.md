Thus, it is advised to use namespaces when necessary without worrying about performance overhead at run-time. However, it is important to note that if one builds unnecessary namespaces, it may affect the readability of the program.

# RECAPITULATION

+   - Use of third-party libraries introduces name conflict problem.
+   - If the functions are grouped and every group is given a specific name, then we can qualify the function as a part of a group.
+   - Namespace is a logical grouping mechanism for grouping objects and qualifying objects by that group to avoid name conflict issues.
+   - Namespace enables the programmer to unambiguously specify the objects of different libraries.
+   - A using declaration can make a single element of the library available to us and a using directive can make the entire library available.
+   - It is possible to use an object of the namespace without the using directive or declaration. In such cases, we can use fully qualified names.
+   - We can define variables, functions, and classes inside namespaces.
+   - It is possible to extend the namespace (except the std namespace) with additional objects.

+   - Unnamed namespace, that is, namespaces without any name is also possible.
+   - Variables defined in unnamed namespaces are available to the program in the same file similar to global static variables.
+   - It is possible to define one namespace inside another one. Such a namespace is known as nested namespace.
+   - A long namespace name can be shortened by using namespace alias.
+   - When the user does not specify the namespace name for any object, it is possible for a compiler to apply argument-dependent lookup algorithm to find that namespace name from the context. This algorithm is popularly known as the Koenig lookup algorithm.
+   - Namespaces incur no overhead at run-time as all processing related to the namespaces is resolved at compile time.

# KEYWORDS

Fully qualified name This is the name of any object, variable, or function with the names of the namespace and the scope resolution operator (::).

Global namespace This is the namespace where every function or class is copied in older C++ by default.

Koenig lookup The ability of the compiler to find the exact namespace of the object in use even when not specified by the programmer is known as Koenig lookup.

Namespace This is an enclosure of logical nature, which helps libraries to have separate existence and solves the name conflict problem.

Namespace aliases A shorter name given to a long fully qualified name using namespace aliasing syntax is known as a namespace alias for the long fully qualified name. This process is known as namespace aliasing.

Nested namespaces Namespaces defined inside another are known as nested namespaces.

Unnamed namespace This is a namespace without any name specified for it. It is now recommended to use unnamed namespaces in place of global static variables.

using declaration This is a mechanism for making a single element of a library available to the program.

using directive This is a mechanism for making all elements of a library available to the program at a single stretch.