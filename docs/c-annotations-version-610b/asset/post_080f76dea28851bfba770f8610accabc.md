
Default template parameter values (either type or non-type template parameters) may not be specified when defining template member functions. In general: function template definitions (and thus: class template member functions) may not be given default template (non-)type arguments. If default template arguments are to be used for class template members, they *have* to be specified by the class interface.

Similar to non-type parameters of function templates, default argument values for non-type class template parameters may only be specified as constants:

- Global variables have constant addresses, which can be used as arguments for non-type parameters.
- Local and dynamically allocated variables have addresses that are *not* known by the compiler when the source file is compiled. These addresses can therefore *not* be used as arguments for non-type parameters.
- Lvalue transformations are allowed: if a pointer is defined as a non-type parameter, an array name may be specified.
- Qualification conversions are allowed: a pointer to a non-const object may be used with a non-type parameter defined as a const pointer.
- Promotions are allowed: a constant of a 'narrower' data type may be used when specifying a default argument for a non-type parameter of a 'wider' type (e.g., a `short` can be used when an `int` is called for, a `long` when a `double` is called for).
- Integral conversions are allowed: if a `size_t` parameter is specified, an `int` may be used as well.
- Variables cannot be used to specify template non-type parameters as their values are not constant expressions. Variables defined using the `const` modifier, however, may be used as their values never change.

Although our attempts to define a constructor of the class `CirQue` accepting an array as its argument have failed so far, we're not yet out of options. In the next section a method is described that *does* allow us to reach our goal.

### 21.1.3 Member templates

Our previous attempt to define a template non-type parameter that is initialized by the compiler to the number of elements of an array failed because the template's parameters are not implicitly deduced when a constructor is called. Instead, they must explicitly be specified when an object of the class template is defined. As the template arguments are specified just before the template's constructor is called, the compiler doesn't have to deduce anything and it can simply use the explicitly specified template arguments.

In contrast, when *function* templates are used, the actual template parameters are deduced from the arguments used when calling the function. This opens up an alley leading to the solution of our problem. If the constructor itself is turned into a function template (having its own template header), then the compiler *will* be able to deduce the non-type parameter's value and there is no need anymore to specify it explicitly using a class template non-type parameter.

Members (functions or nested classes) of class templates that are themselves templates are called *member templates*.

Member templates are defined as any other template, including its own template header.

When converting our earlier `CirQue(Data const (&array)[Size])` constructor into a member template the class template's `Data` type parameter can still be used, but we must provide the member template with a non-type parameter of its own. Its declaration in the (partially shown) class interface looks like this:

```cpp
template <typename Data>
class CirQue
{
    public:
        template <size_t Size>
        explicit CirQue(Data const (&arr)[Size]);
};
```

Its implementation becomes:

```cpp
template <typename Data>
template <size_t Size>
CirQue<Data>::CirQue(Data const (&arr)[Size])
:
    d_size(0),
    d_maxSize(Size),
    d_data(static_cast<Data *>(operator new(sizeof(arr)))),
    d_front(d_data),
    d_back(d_data)
{
    std::copy(arr, arr + Size, back_inserter(*this));
}
```

The implementation uses the STL’s `copy` algorithm and a `back_inserter` adapter to insert the array’s elements into the `CirQue`. To use the `back_inserter`, `CirQue` must define two (public) typedefs (cf. section [18.2.1](#)).

```cpp
typedef Data value_type;
typedef value_type const & const_reference;
```

Member templates have the following characteristics:

- Two template headers must be used: the class template’s `template` header is specified first followed by the member template’s template header;
- Normal access rules apply: the member template can be used by programs to construct a `CirQue` object of a given data type. As usual for class templates, the data type must be specified when the object is constructed. To construct a `CirQue` object from the array `array[30]` we define:

  ```cpp
  CirQue<int> object(array);
  ```

- Any member can be defined as a member template, not just a constructor;
- When a template member is implemented below its class interface, the template class header must precede the function template header of the member template;
- The implementation of the member template must specify its proper scope. The member template is defined as a member of the class `CirQue`, instantiated for the formal template parameter type `Data`;
- The template parameter names in the declaration and implementation must be identical;
- The member template should be defined inside its proper namespace environment. The organization of files defining class templates within a namespace should therefore be:

```cpp
namespace SomeName
{
    template <typename Type, ...>  // class template definition
    class ClassName
    {
        ...
    };

    template <typename Type, ...>    // non-inline member definition(s)
    ClassName<Type, ...>::member(...)
    {
        ...
    }
}                                  // namespace closes
```

A potentially occurring problem remains. Assume that in addition to the above member template a `CirQue<Data>::CirQue(Data const *data)` has been defined. Some (heretofore unelaborated) protocol could be defined allowing the constructor to determine the number of elements that should be stored in the `CirQue` object. When we now define

```cpp
CirQue<int> object(array);
```

it is this latter constructor, rather than the member template, that the compiler will use.

The compiler selects this latter constructor as it is a more specialized version of a constructor of the class `CirQue` than the member template (cf. section 20.14). Problems like these can be solved by defining the constructor `CirQue(Data const *data)` into a member template as well or by defining a constructor using two parameters, the second parameter defining the number of elements to copy.

When using the former constructor (i.e., the member template) it must define a template type parameter `Data2`. Here ‘Data’ cannot be used, as template parameters of a member template may not shadow template parameters of its class. Using `Data2` instead of `Data` takes care of this subtlety. The following declaration of the constructor `CirQue(Data2 const *)` could appear in CirQue’s header file:

```cpp
template <typename Data>
class CirQue
{
    template <typename Data2>
    explicit CirQue(Data2 const *data);
};
```

Here is how the two constructors are selected in code defining two `CirQue` objects:

```cpp
int main()
{
    int array[30];
    int *iPtr = array;

    CirQue<int> ac(array);       // calls CirQue(Data const (&arr)[Size])
    CirQue<int> acPtr(iPtr);     // calls CirQue(Data2 const *)
}
```

### 21.1.4 CirQue’s constructors and member functions

It’s time to return to CirQue’s design and construction again.

The class `CirQue` offers various member functions. Normal design principles should be adhered to when constructing class template members. Class template type parameters should preferably be defined as `Type const &`, rather than `Type`, to prevent unnecessary copying of large data structures. Template class constructors should use member initializers rather than member assignment within the body of the constructors. Member function definitions should preferably not be provided in-class
