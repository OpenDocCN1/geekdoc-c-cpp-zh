specializations:

Click here to view code image

```
template<typename T>
class C;
...
template<typename T = int>
class C<T*>; // ERROR
```

+   - Parameter packs:

Click here to view code image

```
template<typename... Ts = int> struct X; // ERROR
```

+   - The out-of-class definition of a member of a class template: Click here to view code image

```
template<typename T> struct X
{
T f();
};

template<typename T = int> T X<T>::f() { // ERROR
...
}
```

+   - A friend class template declaration:

Click here to view code image

```
struct S {
template<typename = void> friend struct F;
};
```

+   - A friend function template declaration unless it is a definition and no declaration of it appears anywhere else in the translation unit: Click here to view code image

```
struct S {
template<typename = void> friend void f(); // ERROR: not a definition
template<typename = void> friend void g() { //OK so far
}
};
template<typename> void g(); // ERROR: g() was given a default template argument
// when defined; no other declaration may exist here
```

# 12.3 Template Arguments

When instantiating a template, template parameters are substituted by template