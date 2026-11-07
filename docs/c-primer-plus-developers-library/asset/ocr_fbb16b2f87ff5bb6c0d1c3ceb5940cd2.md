rather than alphabetically. What is needed is a class definition that uses `strcmp()` instead of `>`. In such a case, you can provide an explicit template specialization. This takes the form of a template defined for one specific type instead of for a general type. When faced with the choice of a specialized template and a general template that both match an instantiation request, the compiler uses the specialized version.

A specialized class template definition has the following form:

```
template <> class Classname<specialized-type-name> { ... };
```

Older compilers may only recognize the older form, which dispenses with the `template <>` prefix:

```
class Classname<specialized-type-name> { ... };
```

To provide a SortedArray template specialized for the `const char *` type, using the current notation, you would use code like the following:

```
template <> class SortedArray<const char *>
{
    ...// details omitted
};
```

Here the implementation code would use `strcmp()` instead of `>` to compare array values. Now, requests for a SortedArray template of `const char *` will use this specialized definition instead of the more general template definition:

```
SortedArray<int> scores;              // use general definition
SortedArray<const char *> dates;      // use specialized definition
```

# Partial Specializations

C++ allows for *partial specializations*, which partially restrict the generality of a template. For example, a partial specialization can provide a specific type for one of the type parameters:

```
// general template
    template <class T1, class T2> class Pair {...};
// specialization with T2 set to int
    template <class T1> class Pair<T1, int> {...};
```

The `<>` following the keyword `template` declares the type parameters that are still unspecialized. So the second declaration specializes T2 to int but leaves T1 open. Note that specifying all the types leads to an empty bracket pair and a complete explicit specialization:

```
// specialization with T1 and T2 set to int
    template <> class Pair<int, int> {...};
```

The compiler uses the most specialized template if there is a choice. Here’s what would happen given the preceding three templates: