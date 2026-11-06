Assume we extend our design of the class template CirQue so that it defines a second (non-type) parameter size_t Size. Our intent is to use this Size parameter in the constructor defining an array parameter of Size elements of type Data.

The CirQue class template now becomes (only showing the relevant constructor):

```
```cpp
template <typename Data, size_t Size>
class CirQue
{
    // ... data members
    public:
        CirQue(Data const (&arr)[Size]);
        ...
};

template <typename Data, size_t Size>
CirQue<Data, Size>::CirQue(Data const (&arr)[Size])
:
    d_maxSize(Size),
    d_size(0),
    d_data(operator new(Size * sizeof(Data))),
    d_front(d_data),
    d_back(d_data),
{
    std::copy(arr, arr + Size, back_inserter(*this));
}
```
```

Unfortunately, this setup doesn't satisfy our needs as the values of template non-type parameters are not deduced by the compiler. When the compiler is asked to compile the following main function it reports a mismatch between the required and actual number of template parameters:

```
```cpp
int main()
{
    int arr[30];

    CirQue<int> ap(arr);

}
/*
    Error reported by the compiler:

    In function 'int main()':
        error: wrong number of template arguments (1, should be 2)
        error: provided for 'template<class Data, size_t Size>
            class CirQue'
*/
```
```

Defining Size as a non-type parameter having a default value doesn't work either. The compiler always uses the default unless its value is explicitly specified. Reasoning that Size can be 0 unless we need another value, we might be tempted to specify size_t Size = 0 in the template's parameter type list. Doing so we create a mismatch between the default value 0 and the actual size of the array arr as defined in the above main function. The compiler, using the default value, reports:

```
```cpp
In instantiation of 'CirQue<int, 0>':
...
error: creating array with size zero ('0')
```
```

So, although class templates may use non-type parameters they must always be specified like type parameters when an object of that class is defined. Default values can be specified for such non-type parameters causing the compiler to use the default when the non-type parameter is left unspecified.