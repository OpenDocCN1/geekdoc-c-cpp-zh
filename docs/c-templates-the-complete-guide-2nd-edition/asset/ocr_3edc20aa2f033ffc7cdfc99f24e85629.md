```
// partial specialization: both template parameters have same type
template<typename T>
class MyClass<T,T> {
    ...
};
```

```
// partial specialization: second type is int
template<typename T>
class MyClass<T,int> {
    ...
};
```

```
// partial specialization: both template parameters are pointer types
template<typename T1, typename T2>
class MyClass<T1*,T2*> {
    ...
};
```