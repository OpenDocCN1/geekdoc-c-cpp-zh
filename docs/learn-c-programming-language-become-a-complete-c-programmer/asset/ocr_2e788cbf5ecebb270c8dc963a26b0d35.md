```
```cpp
template<bool B, typename T>
using Enable_if = typename std::enable_if<B,T>::type;
template<typename T> bool Is_class()
{
  return std::is_class<T>::value;
}
```
```

If **Enable_if**’s condition evaluates to **true**, its result is its second argument (here, **T**). If **Enable_if**’s condition evaluates to **false**, the whole function declaration of which it is part is completely ignored. In this case, if **T** is a class, we get a definition of **operator->()** returning a **T***, and if it is not, we don’t declare anything.

Given the definition of **Smart_pointer** using **Enable_if**, we get:

```
```cpp
void f(Smart_pointer<double> p, Smart_pointer<complex<double>> q)
{
  auto d0 = *p; // OK
  auto c0 = *q; // OK
  auto d1 = q->real(); // OK
  auto d2 = p->real(); // error: p doesn’t point to a class object
  // ...
}
```
```

You may consider **Smart_pointer** and **operator->()** exotic, but providing (defining) operations conditionally is very common. The standard library provides many examples of conditional definition, such as **Alloc::size_type** (§34.4.2) and **pair** being movable if both of their elements are (§34.2.4.1). The language itself defines-> only for pointers to class objects (§8.2).

# Section 28.4 Conditional Definition: **Enable_if** 797

In this case, the elaboration of the declaration of **operator->()** with **Enable_if** simply changes the kind of error we get from examples, such as **p->real()**:

+   - If we unconditionally declare **operator->()**, we get a “**-> used on a non-class pointer**” error at instantiation time for the definition of **Smart_pointer<double>::operator->()**.
+   - If we conditionally declare **operator->()** using **Enable_if**,ifwe-> on a **smart_ptr<double>**, we get a “**Smart_ptr<double>::operator->() not defined**” error at the point of use of **Smart_ptr<double>::operator->()**.

In either case, we do not get an error unless we use-> on a **smart_ptr<T>** where T is not a class.

We have moved the error detection and reporting from the implementation of **smart_pointer<T>::operator->()** to its declaration. Depending on the compiler and especially on how deep in a nest of template instantiations the error happens, this can make a significant difference. In general, it is preferable to specify templates precisely so as to detect errors early rather than relying on bad instantiations being caught. In this sense, we can see **Enable_if** as a variant of the idea of a concept (§24.3): it allows a more precise specification of the requirements of a template.

# 28.4.1 Use of **Enable_if**