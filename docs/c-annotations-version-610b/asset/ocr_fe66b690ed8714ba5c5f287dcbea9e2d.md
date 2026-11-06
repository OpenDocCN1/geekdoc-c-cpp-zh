```
```cpp
d_front->Data();
d_front = inc(d_front);
}
operator delete(d_data);
}
```
```

Here are CirQue’s members:

+   - `CirQue &operator=(CirQue<Data> const &other):`

The copy assignment operator has a standard implementation:

```
```cpp
template<typename Data>
CirQue<Data> &CirQue<Data>::operator=(CirQue<Data> const &rhs)
{
    CirQue<Data> tmp(rhs);
    swap(tmp);
}
```
```

+   - `CirQue &operator=(CirQue<Data> & &&tmp):`

The move assignment operator also has a standard implementation. As its implementation merely calls swap it is defined as an inline function template:

```
```cpp
template<typename Data>
inline CirQue<Data> &CirQue<Data>::operator=(CirQue<Data> & &&tmp)
{
    swap(tmp);
}
```
```

+   - `void pop_front():`

removes the element pointed at by `d_front` from the CirQue. Throws an exception if the CirQue is empty. The exception is thrown as a `CirQue<Data>::EMPTY` value, defined by the `enum CirQue<Data>::Exception` (see push_back). The implementation is straightforward (explicitly calling the destructor of the element that is removed):

```
```cpp
template<typename Data>
void CirQue<Data>::pop_front()
{
    if (d_size == 0)
        throw EMPTY;

    d_front->~Data();
    d_front = inc(d_front);
    --d_size;
}
```
```

+   - `void push_back(Data const &object):`

adds another element to the CirQue. Throws a `CirQue<Data>::FULL` exception if the CirQue is full. The exceptions that can be thrown by a CirQue are defined in its Exception enum:

```
```cpp
enum Exception
{
    EMPTY,
    FULL
};
```
```

A copy of object is installed in the CirQue’s raw memory using placement new and its `d_size` is incremented.

```
```cpp
template<typename Data>
```
```