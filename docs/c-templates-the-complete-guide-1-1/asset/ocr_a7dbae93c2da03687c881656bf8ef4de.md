```
```cpp
extern "C" template<typename T>
void validate();        // ERROR: template cannot have C
extern "C" class template<typename T>
void validate();        // redundant, but maybe some
                        // compiler will accept
// C++ language linkage
```
```

Templates usually have external linkage. The only exceptions are names of templates declared in an unnamed namespace (which have internal linkage), and member templates of unnamed classes (which have no linkage). For example:

Click here to view code image

```
```cpp
template<typename T>       // refers to the same entity as
void validate(T);          // the declaration in the
                           // outer namespace
                           // (same name and scope in an-
                           // other file)
```
```

```
```cpp
template<typename T>       // unrelated to a template with
void validate(T);          // external linkage
                           // (different entity)
```
```

```
```cpp
template<typename T>       // redeclaration of the previous
void validate(T);          // declaration
                           // (same entity)
```
```

```
```cpp
namespace {
template<typename T>
void validate(T); // another file, one
                  // that is in an unnamed namespace
}
```
```

```
```cpp
namespace {
template<typename T>       // redeclaration of the previous
void validate(T);          // declaration
                           // (same entity)
}
```
```

```
```cpp
struct {
  template<typename T> void f(T) { }  // no linkage: cannot
                                      // be redeclared
};
```
```

Note that the latter member template has no linkage; it must be defined within the unnamed class because there is no way to provide a definition outside the class.

Currently templates cannot be declared in function scope or local class scope, but generic lambdas (see Section 6.5.4 on page 243), which have an associated unique closure type, offer a kind of local template: a member function template of a local lambda class, which effectively takes a kind of local member function template.

The linkage of an instance of a template is that of the template. For example, a function template's `void f()` instantiated from the template `template<typename T> void f(T)` above will have internal linkage. This has an interesting consequence in the case of variable templates. Indeed, consider the following example:

Click here to view code image

```
```cpp
template<typename T> T x = T();
```
```

All instantiations of `x` have external linkage, even something like `X<int> x1;` That's perhaps a surprising conclusion.

Click here to view code image

```
```cpp
struct X {
  int x = 10;
};
```
```

has internal linkage, despite its `x` being a template. Similarly, all instantiations of the template:

Click here to view code image

```
```cpp
template<typename T> int const max_value = 10;
```
```

have external linkage, despite all those instantiations also having type `int const`.

# ### 12.2.1.3 Primary Templates

Normal declarations of templates declare primary templates. Such template declarations are declared without adding template arguments to any template name after the template name:

Click here to view code image

```
```cpp
template<typename T> class Box;            // OK: pri-
                                           // mary template
template<typename T> class Box<T>;         // ERROR:
                                           // does not specialize
template<typename T> void validate(T);     // OK: pri-
                                           // mary template
template<typename T> void validate<T>(T);  // ERROR:
                                           // not allowed for functions
template<typename T> T const max_value = T(); // OK:
                                               // primary template
template<typename T> T const max_value<T> = T(); // ERROR:
                                                  // does not specialize
```
```

Nonstatic member templates whose ending partial specializations of the enclosing class template, have...