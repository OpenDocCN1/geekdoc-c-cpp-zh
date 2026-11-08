```
```cpp
extern int count;              // #2

int lookup_example(int count)   // #2
{
    if (count < 0) {
        int count = 1;          // #3
        lookup_example(count);  // unqualified count
    }
    return count + 1;           // the first (unqualified)
}
count refers to #1
```
```

A more recent twist to the lookup of unqualified names is that an additional distinction to ordinary lookup—they may sometimes undergo argument-dependent lookup (ADL). Before proceeding with the details of ADL, let's motivate the mechanism with our perennial max() template.

```
```cpp
template<typename T>
T max (T a, T b)
{
    return b < a ? a : b;
}
```
```

Suppose now that we need to apply this template to a type defined in another namespace:

Click here to view code image

```
```cpp
namespace BigMath {
    class BigNumber {
        ...
    };
}

void operator< (BigNumber const&, BigNumber const&)
{
    ...
}
```
```

```
```cpp
using BigMath::BigNumber;

void g(BigNumber const& a, BigNumber const& b)
{
    ...
    BigNumber x = max(a,b);
    ...
}
```
```

The problem here is that the max() template is unaware of the BigMath namespace, but ordinary lookup would not find the operator < applicable to values of type BigNumber. Without some special rules, this greatly reduces the applicability of templates in the presence of C++ namespaces. ADL is the C++ answer to those "special rules."

# 13.2.1 Argument-Dependent Lookup

ADL applies primarily to unqualified names that look like they name a nonmember function in a function call or operator invocation. ADL does not happen if ordinary lookup finds

+   - the name of a member function,
+   - the name of a variable,
+   - the name of a type, or
+   - the name of a block-scope function declaration.

ADL is also inhibited if the name of the function to be called is enclosed in parentheses.

Otherwise, if the name is followed by a list of argument expressions enclosed in parentheses, ADL proceeds by looking up the name in namespaces and classes "associated with" the types of the call arguments. The precise definition of these associated namespaces and associated classes is given, but intuitively they can be thought of as being all the namespaces and classes that are fairly directly connected to a given type. For example, if the type is a pointer to a class X, then the associated classes and namespace would include X as well as any namespaces or classes to which X belongs.

The precise definition of the set of associated namespaces and associated classes for a given type is described by the following rules:

+   - For built-in types, this is the empty set.
+   
+   - For pointer and array types, the set of associated namespaces and classes is that of the underlying type.
+   
+   - For enumeration types, the associated namespace is the namespace in which the enumeration is declared.
+   
+   - For class types (including union types), the set of associated classes is the type itself, the enclosing classes, and any direct and indirect base classes. The set of associated namespaces is the namespaces in which the associated classes are declared. If the class is a class template instance, then the types of the template type arguments and the classes and namespaces in which those template arguments are declared are also included.
+   
+   - For function types, the sets of associated namespaces and classes comprise the namespaces and classes associated with the parameter types and those associated with the return type.
+   
+   - For pointer-to-member data/function types, the sets of associated namespaces and classes comprise the namespaces and classes associated with the class and the type of the member. (If it is a pointer-to-member ...)