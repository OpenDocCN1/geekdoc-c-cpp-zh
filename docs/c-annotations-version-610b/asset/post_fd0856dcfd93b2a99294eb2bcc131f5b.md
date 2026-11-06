
### 22.8.5.3 Erasing all occurrences of a type

Erasing all occurrences of type EraseType from a Typelist can easily be accomplished by applying the erase procedure not only to the head of the Typelist but also to the Typelist's tail.

Here is the algorithm, described in a slightly different order than Erase's algorithm:

- If the Typelist is empty, there's nothing to erase, and an empty Typelist results. This is exactly what we do with Erase, so we can use inheritance to prevent us from having to duplicate elements of a template meta program:

```cpp
template <typename EraseType>
struct Erase<EraseType, Typelist<>>
{
    typedef Typelist<> List;
};
```

- The foundation of the algorithm is therefore a struct template EraseAll expecting the type to erase and a Typelist that is derived from Erase, thus already offering the empty Typelist handling specialization:

```cpp
template <typename EraseType, typename Typelist>
struct EraseAll: public Erase<EraseType, Typelist>
{};
```

- If Typelist's head matches EraseType, EraseAll is also applied to the Typelist's tail, thus removing all occurrences of EraseType from Typelist:

```cpp
template <typename EraseType, typename ...Tail>
struct EraseAll<EraseType, Typelist<EraseType, Tail...>>
{
    typedef typename EraseAll<EraseType, Typelist<Tail...>>::List List;
};
```

- In all other cases (i.e., Typelist's head does *not* match EraseType), EraseAll is applied to the Typelist's tail. The returned Typelist consists of the original Typelist's initial type and the types of the Typelist returned by the recursive EraseAll call:

```cpp
template <typename EraseType, typename Head, typename ...Tail>
struct EraseAll<EraseType, Typelist<Head, Tail...>>
{
    typedef typename Prefix<
        Head,
        typename EraseAll<EraseType, Typelist<Tail...>>::List
    >::List List;
};
```

Here is a statement showing how EraseAll can be used:

```cpp
cout <<
    "After erasing size_t from "
    "Typelist<char, int, size_t, double, size_t>\n"
    "it contains " <<
        EraseAll<size_t,
            Typelist<char, int, size_t, double, size_t>
        >::List::size << " types\n";
```

### 22.8.5.4 Erasing duplicates

To remove all duplicates from a TypeList all the TypeList’s first elements must be erased from the TypeList’s tail, applying the procedure recursively to the TypeList’s tail. The algorithm, outlined below, merely expects a TypeList:

- First, the generic EraseDup struct template is declared. EraseDup structures define a type List representing the TypeList that they generate. EraseDup calls expect a TypeList as their template type parameters:

```cpp
template <typename TypeList>
struct EraseDup;
```

- If the TypeList is empty it can be returned empty and we’re done:

```cpp
template <>
struct EraseDup<TypeList<>>
{
    typedef TypeList<> List;
};
```

- In all other cases
  - EraseDup is first applied to the original TypeList’s tail. By definition this results in a TypeList from which all duplicates have been removed;
  - The TypeList returned by the previous step might contain the original TypeList’s initial type. If so, it is removed by applying Erase on the returned TypeList, specifying the original TypeList’s initial type as the type to remove;
  - The returned TypeList consists of the original TypeList’s initial type to which the types of the TypeList produced by the previous step are appended.

This specialization is implemented like this:

```cpp
template <typename Head, typename ...Tail>
struct EraseDup<TypeList<Head, Tail...>>
{
    typedef typename EraseDup<TypeList<Tail...>>::List UniqueTail;
    typedef typename Erase<Head, UniqueTail>::List NewTail;

    typedef typename Prefix<Head, NewTail>::List List;
};
```

Here is an example showing how EraseDup can be used:

```cpp
cout <<
    "After erasing duplicates from "
        "TypeList<double, char, int, size_t, int, double, size_t>\n"
    "it contains " <<
    EraseDup<
        TypeList<double, char, int, size_t, int, double, size_t>
    >::List::size << " types\n";
```

## 22.9 Using a TypeList

In the previous sections the definition and some of the features of typelists were discussed. Most C++ programmers consider typelists both exciting and an intellectual challenge, honing their skills in the area of recursive programming.

```cpp
struct Vector : public std::vector<Type>
{
    Vector(std::initializer_list<Type> iniValues)
    :
        std::vector<Type>(iniValues)
    {}
};
```

Now Vector provides std::vector’s second parameter using its default template argument. Alternatively, a *template using* declaration could be used.

- If the TypeList contains two types like `int` and `double` and the policy class is Vector, then the MultiBase class eventually inherits from `vector<int>` and `vector<double>`. But if the TypeList contains identical types, like two `int` type specifications, MultiBase would inherit from two `vector<int>` classes. Classes cannot be derived from identical base classes as that would make it impossible to distinguish among their members. Regarding this, Alexandrescu (2001) writes (p.67):

> *There is one major source of annoyance...: you cannot use it when you have duplicate types in your TypeList.*  
> *.... There is no easy way to solve the ambiguity, [as the eventually derived class /FBB] ends up inheriting [the same base class /FBB] twice.*

There is a way around the problem of duplicate base class types. If, instead of inheriting directly from base classes, these base classes are first wrapped in unique type defining classes, then these unique classes can be used to access the base classes using principles of inheritance. As these unique type-defining wrapper classes are merely classes that are derived from the ‘real’ base classes they inherit (and thus: offer) the functionality of their base classes. A unique type defining wrapper class can be designed after the class IntType, defined earlier. The wrapper class we’re looking combines class derivation with the uniqueness offered by IntType. The class template UWrap has two template parameters: one non-type parameter idx and one type parameter Type. By ensuring that each UWrap definition uses a unique idx value, unique class types are created. These unique class types are then used as base classes of the derived class MultiBase:

```cpp
template <size_t nr, typename Type>
struct UWrap: public Type
{
    UWrap(Type const &type)
    :
        Type(type)
    {}
};
```

Using UWrap it’s easy to distinguish, e.g., two `vector<int>` classes: `UWrap<0, vector<int>>` could refer to the first `vector<int>`, `UWrap<1, vector<int>>` to the second vector.

Uniqueness of the various UWrap types is assured by the class template MultiBase as discussed in the next section.

It must also be possible to initialize a Multi class object. Its constructor therefore expects the initialization values for all its Policy values. So if a Multi is defined for Vector, int, string then its constructor can receive the matching initialization values. E.g.,

```cpp
Multi<vector, int, string> mvis({1, 2, 3}, {"one", "two", "three"});
```

### 22.9.2 The MultiBase class template

The class template MultiBase is Multi’s base class. It defines a class that, eventually, is derived from the list of Policy types that, in turn, were created by Multi using any additional types that were passed to it.

![](img/859c398c8f9601f32700b78894504b0a_686_0.png)

Figure 22.1: Layout of a MultiBase class hierarchy

MultiBase itself has no concept of a Policy. To MultiBase the world appears to consist of a simple template pack whose types are used to define a class from. In addition to the PolicyTypes template pack, MultiBase also defines a `size_t nr` non-type parameter that is used to create unique UWrap types. Here is MultiBase’s generic class declaration:

```cpp
template <size_t nr, typename ...PolicyTypes>
struct MultiBase;
```

Two specializations handle all possible MultiBase invocations. One specialization is a recursive template. This template handles the first type of MultiBase’s template parameter pack and recursively uses itself to handle the remaining types. The second specialization is invoked once the template parameter pack is exhausted and does nothing. Here is the definition of the latter specialization:

```cpp
template <size_t nr>
struct MultiBase<nr>
{};
```

The recursively defined specialization is the interesting one. It performs the following tasks:

- It is derived from a unique UWrap type. The uniqueness is guaranteed by using MultiBase’s nr parameter when defining UWrap. In addition to nr, the UWrap class receives the first type of the template parameter pack made available to MultiBase;
- It is also recursively derived from itself. The recursive MultiBase type is defined using as its first template argument an incremented nr value (thus ensuring the uniqueness of the UWrap types defined by recursive MultiBase types). Its second template argument is the tail of the template parameter pack made available to MultiBase.

An illustration showing the layout of the MultiBase class hierarchy is provided in figure 22.1.

MultiBase’s constructor simply receives the initialization values that were (originally) passed to the MultiBase object. Perfect forwarding is used to accomplish this. MultiBase’s constructor passes its first parameter value to its UWrap base class, also using perfect forwarding. MultiBase’s recursive definition is:

```cpp
template <size_t nr, typename PolicyT1, typename ...PolicyTypes>
```
