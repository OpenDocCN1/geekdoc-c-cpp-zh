```
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

```
CirQue<int> object(array);
```

it is this latter constructor, rather than the member template, that the compiler will use.

The compiler selects this latter constructor as it is a more specialized version of a constructor of the class `CirQue` than the member template (cf. section 20.14). Problems like these can be solved by defining the constructor `CirQue(Data const *data)` into a member template as well or by defining a constructor using two parameters, the second parameter defining the number of elements to copy.

When using the former constructor (i.e., the member template) it must define a template type parameter `Data2`. Here ‘Data’ cannot be used as template parameters of a member template may not shadow template parameters of its class. Using `Data2` instead of `Data` takes care of this subtlety. The following declaration of the constructor `CirQue(Data2 const *)` could appear in CirQue’s header file:

```
template <typename Data>
class CirQue
{
    template <typename Data2>
    explicit CirQue(Data2 const *data);
}
```

Here is how the two constructors are selected in code defining two `CirQue` objects:

```
int main()
{
    int array[30];
    int *iPtr = array;

    CirQue<int> ac(array);       // calls CirQue(Data const (&arr)[Size])
    CirQue<int> acPtr(iPtr);     // calls CirQue(Data2 const *)
}
```

# 21.1.4  CirQue’s constructors and member functions

It’s time to return to Cirque’s design and construction again.

The class `CirQue` offers various member functions. Normal design principles should be adhered to when constructing class template members. Class template type parameters should preferably be defined as `Type const &`, rather than `Type`, to prevent unnecessary copying of large data structures. Template class constructors should use member initializers rather than member assignment within the body of the constructors. Member function definitions should preferably not be provided in-class