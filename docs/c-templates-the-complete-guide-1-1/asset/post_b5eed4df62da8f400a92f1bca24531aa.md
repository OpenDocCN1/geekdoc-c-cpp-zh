
```cpp
extern "C" template<typename T>
void validate();        // ERROR: template cannot have C
extern "C" class template<typename T>
void validate();        // redundant, but maybe some
                        // compiler will accept
// C++ language linkage
```

Templates usually have external linkage. The only exceptions are names of templates declared in an unnamed namespace (which have internal linkage), and member templates of unnamed classes (which have no linkage). For example:

Click here to view code image

```cpp
template<typename T>       // refers to the same entity as
void validate(T);          // the declaration in the
                           // outer namespace
                           // (same name and scope in an-
                           // other file)
```

Click here to view code image

```cpp
template<typename T>       // unrelated to a template with
void validate(T);          // external linkage
                           // (different entity)
```

Click here to view code image

```cpp
template<typename T>       // redeclaration of the previous
void validate(T);          // declaration
                           // (same entity)
```

Click here to view code image

```cpp
namespace {
template<typename T>
void validate(T); // another file, one
                  // that is in an unnamed namespace
}
```

Click here to view code image

```cpp
namespace {
template<typename T>       // redeclaration of the previous
void validate(T);          // declaration
                           // (same entity)
}
```

Click here to view code image

```cpp
struct {
  template<typename T> void f(T) { }  // no linkage: cannot
                                      // be redeclared
};
```

Note that the latter member template has no linkage; it must be defined within the unnamed class because there is no way to provide a definition outside the class.

Currently templates cannot be declared in function scope or local class scope, but generic lambdas (see Section 6.5.4 on page 243), which have an associated unique closure type, offer a kind of local template: a member function template of a local lambda class, which effectively is a kind of local member function template.

The linkage of an instance of a template is that of the template. For example, a function template's `void f()` instantiated from the template `template<typename T> void f(T)` above will have internal linkage. This has an interesting consequence in the case of variable templates. Indeed, consider the following example:

Click here to view code image

```cpp
template<typename T> T x = T();
```

All instantiations of `x` have external linkage, even something like `x<int> x1;` That's perhaps a surprising conclusion.

Click here to view code image

```cpp
struct X {
  int x = 10;
};
```

has internal linkage, despite its `x` being a template. Similarly, all instantiations of the template:

Click here to view code image

```cpp
template<typename T> int const max_value = 10;
```

have external linkage, despite all those instantiations also having type `int const`.

### 12.2.1.3 Primary Templates

Normal declarations of templates declare primary templates. Such template declarations are declared without adding template arguments to any template name after the template name:

Click here to view code image

```cpp
template<typename T> class Box;            // OK: primary template
template<typename T> class Box<T>;         // ERROR:
                                           // does not specialize
template<typename T> void validate(T);     // OK: primary template
template<typename T> void validate<T>(T);  // ERROR:
                                           // not allowed for functions
template<typename T> T const max_value = T(); // OK:
                                               // primary template
template<typename T> T const max_value<T> = T(); // ERROR:
                                                  // does not specialize
```

Nonstatic member templates whose ending partial specializations of the enclosing class template, have...

## 12.2 TEMPLATE PARAMETERS

There are three basic kinds of template parameters:

- 1. Type parameters (these are by far the most common)
- 2. Nontype parameters
- 3. Template template parameters

Any of these basic kinds of template parameters can be used as the basis of a complete parameterized type (see Section 12.2.4 on page 188).

Template parameters are declared in the introductory parameterization clause of a template declaration. Such declarations do not necessarily need to be named:

Click here to view code image

```cpp
template<typename, int>
class X;       // X is parameterized by a type and an integer
```

A parameter name is, of course, required if the parameter is referred to later in the template. Note also that a template parameter name can be referred to in a subsequent parameter declaration (but not before):

Click here to view code image

```cpp
template<typename T,             // the first parameter is
         typename T::Root,         // in the declaration of
                                   // the second one, and
         typename T::Root::...>    // in the declaration of
class Structure;                   // the third one
```

### 12.2.1 Type Parameters

Template parameters are introduced with either the keyword typename or the keyword class: The two are entirely equivalent. The keyword must be followed by a simple identifier, and that identifier must be followed by a comma to declare the start of the next parameter declaration, a closing angle bracket (>) to denote the end of the parameterization clause, or an equal sign (=) to denote the beginning of a default template argument.

Within a template declaration, a type parameter acts much like a type alias (see Section 8.2.8 on page 83). For example, it is not possible to use a qualified name of the form T::... before T is a template parameter, even if T were to be substituted by a class type:

Click here to view code image

```cpp
template<typename Allocator>
class List {
    class Allocator*     // ERROR: use
        Allocator allocator;     // ERROR: use
    friend class Allocator;      // ERROR: use "friend
                                 // Allocator"
};
```

### 12.2.2 Nontype Parameters

Nontype template parameters stand for constant values that can be determined at compile time. The type of such a parameter (in other words, the type of the value that it stands for) must be one of the following:

- An integer type or an enumeration type
- A pointer type
- A pointer-to-member type
- An lvalue reference type (both references to objects and references to functions are acceptable)
- std::nullptr_t
- A floating-point type (auto in C++20 only; see Section 15.10.4 on page 296)

All other types are unambiguously excluded (although floating-point types may be added in the future; see Section 17.2 on page 315).

Perhaps surprisingly, the declaration of a nontype template parameter can in some cases also start with the keyword typename:

Click here to view code image

```cpp
template<typename T,       // a type parameter
         T N>               // a nontype
                            // parameter
class List;
```

or with the keyword class:

Click here to view code image

```cpp
template<class T*>       // a nontype parameter of pointer
class X {
    T* p;
};
```

to the pointer type to which they decay:

Click here to view code image

```cpp
template<int N> class Lessor;        // but is not a valid type
template<int* I> class Lessor;        // this is a valid type

template<int fn()> struct FuncWrap;   // fn really has pointer to
                                      // function

template<int (*)()> struct FuncWrap;  // a declaration
```

Non-type template parameters are declared much like variables, but they cannot have non-type specifiers like static, mutable, and so forth. They can have const and volatile qualifiers, but if such a qualifier is used, it is at the outermost level of the parameter type, it is simply ignored:

Click here to view code image

```cpp
template<const int length> class Buffer; // const is useless here
template<int* const Buffer>               // this is previous declaration
void declaration
```

Finally, non-type template parameters are always resolved and used in expressions. Their address cannot be taken, they cannot be assigned to. A non-type parameter of lvalue reference type, on the other hand, can be used to denote any lvalue referenced type, under other circumstances.

Click here to view code image

```cpp
template<class Counter>
struct LocalIncrement {
  Counter& increment() { Counter = Counter + 1; }
  // ...
  ~LocalIncrement() { Counter = Counter - 1; }
};
```

Invalid references are not permitted.

### 12.2.3 Template Parameters

Template template parameters are placeholders for class or alias templates. They are declared much like class templates, but the keywords struct and union can also be used:

Click here to view code image

```cpp
template<typename T>
void f(C<int>* p);

template<typename T> typename <struct C>  // ERROR:
                                          // struct not valid here
void f(C<int>* p);

template<typename T> typename <union C>   // ERROR:
                                          // union not valid here
void f(C<int>* p);
```

C++ allows the use of typename instead of class. That change was motivated by the fact that template template parameters can be substituted not only by class templates but also by alias templates (which instantiate to arbitrary types). So, in C++11, our example above can be written instead as

Click here to view code image

```cpp
template<template<typename> typename C>  // C++11
using C1 = C<int>;
void f(C<int>* p);
```

In the scope of their declaration, template template parameters are used just like other class or alias templates.

The parameters of template templates can have default template arguments. These default arguments apply when the corresponding parameters are not specified in uses of the template parameter:

Click here to view code image

```cpp
template<template<typename T,
                   typename A = std::allocator<T>> class
         Container>
class Adaptation {
  Container<T> storage;  // implicitly equivalent to
                         // Container<T, std::allocator<T>>
};
```

T and A are the names of the template parameter of the template template parameter Container. These names can be used only in the declaration of the template parameter of that template parameter. The following contrived template illustrates this concept:

Click here to view code image

```cpp
template<template<typename T, typename A> class Buf> // OK
class T {
  static T* storage; // template parameter
};
// A template parameter cannot be used here
```

Usually however, the names of the template parameters of a template
