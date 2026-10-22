```
template<template<typename X> typename C> // OK since C++17
void f(C<int>* p);
```