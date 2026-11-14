```
using namespace std;
```

is often the first one in a `main` function or even the first after the includes. Importing `std` in the global namespace has good potential for name conflicts, for instance, when we also define a class named `vector` (in the global namespace).

# Advice

Do not import names or namespaces (outside functions) within header files.

When a namespace's name is too long, especially a nested namespace, we can rename it with a `Namespace Alias`:

![](bbox=[0.15, 0.38, 0.38, 0.4])

```
namespace lname= long_namespace_name;
namespace dvector= algebra::vector::dense;
```

As before, this should be done in an appropriate scope.

![](bbox=[0.54, 0.51, 0.87, 0.53])

# C++17

With the same colon-separated notation, we can open a nested namespace in C++17:

![](bbox=[0.15, 0.59, 0.38, 0.61])

```
namespace algebra::vector::dense {
    class vector3 { /* */ };
}
```

instead of writing nested declarations of single namespaces.

# 3.2.2 Argument-Dependent Lookup

Argument-Dependent Lookup, or ADL, expands the search of function names to the namespaces of their arguments—but not to their respective parent namespaces. This saves us from verbose namespace qualification for functions. Say we write the ultimate scientific library within the modest namespace `rocketscience`:

![](bbox=[0.15, 0.88, 0.38, 0.9])