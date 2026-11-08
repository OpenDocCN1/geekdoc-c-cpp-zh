Here, template argument deduction from the first argument deduces T to int, while deduction from the second argument deduces T to double. Because both parameters are passed by reference, the deduction conflicts and the call is not possible. The same error can arise, however, if you use a parameter that is a common base class:

```
~~~cpp
std::max(static_cast<Base*>(&d1),&d2);
~~~
```

Click here to view code image

would have succeeded.

Perhaps you are wondering if that is the error message you would get. On the first line, the compiler detects the error because both parameters have different types deduced from a common base-class. But if you use a common base class as a common base class, the deduction does not succeed. See Section 1.2 on page 7 for a discussion of this issue and possible solutions.

# ### 15.8.2 CLASS TEMPLATE ARGUMENTS

Prior to C++17, template argument deduction applied exclusively to function and member function templates. In particular, the arguments for a class template were not deduced from the arguments to a call of one of its constructors. For example:

Click here to view code image

```
~~~cpp
template<typename T>
class C {
public:
  C(T b) : a(b) {
  }

private:
  T a;
};

C c(42); // ERROR: Before C++17, the class template parameter T was not deduced from
         //            the constructor call argu-
         //            ment
~~~
```

This limitation is lifted in C++17—see Section 15.10 on page 341.

# ### 15.8.3 DEFAULT CALL ARGUMENTS

Default function call arguments can be specified in function templates just as they are in ordinary functions:

Click here to view code image

```
~~~cpp
template<typename T>
void f(T x = T{}, T y = T{}) {
  T* p = &x;
  ...
}
~~~
```

In fact, as in this example shows, the default function call argument can depend on a template parameter. Such a dependent default argument is prescribed—a principle that makes the following example valid:

Click here to view code image

```
~~~cpp
class B {
public:
  B(int, int);
};

template<typename T>
class D : public B {
public:
  using B::B;
};

D d(1, 2); // OK
~~~
```

Initializing d(1, 2) is an error because B has no constructor B(int, int).

Even when a default call argument is not dependent, it cannot be used to deduce template arguments. This means that the following is invalid C++:

Click here to view code image

```
~~~cpp
template<typename T>
void f(T = 42) {
}

f(); // ERROR: no T
~~~
```

# ### 15.8.4 EXCEPTION SPECIFICATIONS

Like default call arguments, exception specifications are only instantiated when they are used. The reason is that they can be part of a template's signature. For example:

Click here to view code image

```
~~~cpp
template<typename T>
void f(T) noexcept(noexcept(T())) {}
~~~
```