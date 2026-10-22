
```cpp
static int count; //#10
};
void print() const { //#11
}
};
```

The ordinary members code at point #4 and print() at point #5 of the generic Outer template #1 have a single enclosing class template and hence need one template<> prefix to specialize them fully for a specific set of template arguments: Click here to view code image

```cpp
template<>
int Outer<void>::code = 12;

template<>
void Outer<void>::print() const
{
std::cout << "Outer<void>";
}
```

These definitions are used over the generic ones at points #4 and #5 for class Outer<void>, but other members of class Outer<void> are still generated from the template at point #1. Note that after these declarations, it is no longer valid to provide an explicit specialization for Outer<void>.

Just as with full function template specializations, we need a way to declare the specialization of an ordinary member of a class template without specifying a definition (to prevent multiple definitions). Although nondefining out-of-class declarations are not allowed in C++ for member functions and static data members of ordinary classes, they are fine when specializing members of class templates. The previous definitions could be declared with Click here to view code image

```cpp
template<>
int Outer<void>::code;

template<>
void Outer<void>::print() const;
```

The attentive reader might point out that the nondefining declaration of the full specialization of Outer<void>::code looks exactly like a definition to be initialized with a default constructor. This is indeed so, but such declarations are always interpreted as nondefining declarations. For a full specialization of a static data member with a type that can only be initialized using a default constructor, we must resort to initializer list syntax. Given the following: Click here to view code image

```cpp
class DefaultInitOnly {
public:
DefaultInitOnly() = default;
DefaultInitOnly(DefaultInitOnly const&) = delete;
};

template<typename T>
class Statics {
private:
static T sm;
};
```

the following is a declaration:

Click here to view code image

```cpp
template<>
DefaultInitOnly Statics<DefaultInitOnly>::sm;
```

while the following is a definition that calls the default constructor: Click here to view code image

```cpp
template<>
DefaultInitOnly Statics<DefaultInitOnly>::sm{};
```

Prior to C++11, this was not possible. Default initialization was thus not available for such specializations. Typically, an initializer copying a default value was used: Click here to view code image

```cpp
template<>
DefaultInitOnly Statics<DefaultInitOnly>::sm = DefaultInitOnly();
```

Unfortunately, for our example that was not possible because the copy constructor is deleted. However, C++17 introduced mandatory copy-elision rules, which make that alternative valid, because no copy constructor invocation is involved anymore.

The member template Outer<T>::Inner can also be specialized for a given template argument without affecting the other members of the specific instantiation of Outer<T>, for which we are specializing the member template. Again, because there is one enclosing template, we will need one template<> prefix. This results in code like the following: Click here to view code image

```cpp
template<>
template<typename X>
class Outer<wchar_t>::Inner {
public:
static long count; // member type changed
};
```

```cpp
template<>
template<typename X>
long Outer<wchar_t>::Inner<X>::count;
```

The template Outer<T>::Inner can also be fully specialized, but only for a given instance of Outer<T>. We now need two template<> prefixes: one because of the enclosing class and one because we’re fully specializing the inner template: Click here to view code image

```cpp
template<>
template<>
class Outer<char>::Inner<wchar_t> {
public:
enum { count = 1 };
};

// the following is not valid C++:
// template<> cannot follow a template parameter list
template<typename X>
template<> class Outer<X>::Inner<void>; // ERROR
```

Contrast this with the specialization of the member template of Outer<bool>. Because the latter is already fully specialized, there is no enclosing template, and we need only one template<> prefix: Click here to view code image

```cpp
template<>
class Outer<bool>::Inner<wchar_t> {
public:
enum { count = 2 };
};
```

## 16.4 Partial Class Template Specialization

Full template specialization is often useful, but sometimes it is natural to want to specialize a class template or variable template for a family of template arguments rather than just one specific set of template arguments. For example, let’s assume we have a class template implementing a linked list: Click here to view code image

```cpp
template<typename T>
class List { // #1
public:
...
void append(T const&);
inline std::size_t length() const;
...
};
```

A large project making use of this template may instantiate its members for many types. For member functions that are not expanded inline (say, List<T>::append()), this may cause noticeable growth in the object code. However, we may know that from a low-level point of view, the code for List<int*>::append() and List<void*>::append() is the same.

In other words, we’d like to specify that all Lists of pointers share an implementation. Although this cannot be expressed in C++, we can achieve something quite close by specifying that all Lists of pointers should be instantiated from a different template definition: Click here to view code image

```cpp
template<typename T>
class List<T*> { // #2
private:
List<void*> impl;
...
public:
...
inline void append(T* p) {
impl.append(p);
}
inline std::size_t length() const {
return impl.length();
}
...;
};
```

In this context, the original template at point #1 is called the primary template, and the latter definition is called a partial specialization (because the template arguments for which this template definition must be used have been only partially specified). The syntax that characterizes a partial specialization is the combination of a template parameter list declaration (template<...>) and a set of explicitly specified template arguments on the name of the class template (<T*> in our example).

Our code contains a problem because List<void*> recursively contains a member of that same List<void*> type. To break the cycle, we can precede the previous partial specialization with a full specialization: Click here to view code image

```cpp
template<>
class List<void*> { // #3
...
void append (void* p);
inline std::size_t length() const;
...;
};
```

This works because matching full specializations are preferred over partial specializations. As a result, all member functions of Lists of pointers are forwarded (through easily inlineable functions) to the implementation of List<void*>. This is an effective way to combat code bloat (of which C++ templates are often accused).

There exist several limitations on the parameter and argument lists of partial specialization declarations. Some of them are as follows:

1. The arguments of the partial specialization must match in kind (type, nontype, or template) the corresponding parameters of the primary template.
2. The parameter list of the partial specialization cannot have default arguments; the default arguments of the primary class template are used instead.
3. The nontype arguments of the partial specialization should be either nondependent values or plain nontype template parameters. They cannot be more complex dependent expressions like 2*N (where N is a template parameter).
4. The list of template arguments of the partial specialization should not be identical (ignoring renaming) to the list of parameters of the primary template.
5. If one of the template arguments is a pack expansion, it must come at the end of a template argument list.

An example illustrates these limitations:

Click here to view code image

```cpp
template<typename T, int I = 3>
class S; // primary template

template<typename T>
class S<int, T>; // ERROR: parameter kind mismatch

template<typename T = int>
class S<T, 10>; // ERROR: no default arguments

template<int I>
class S<int, I*2>; // ERROR: no nontype expressions

template<typename U, int K>
class S<U, K>; // ERROR: no significant difference from primary template

template<typename... Ts>
class Tuple;

template<typename Tail, typename... Ts>
class Tuple<Ts..., Tail>; // ERROR: pack expansion not at the end

template<typename Tail, typename... Ts>
class Tuple<Tuple<Ts...>, Tail>; // OK: pack expansion is at the end of a
// nested template argument list
```

Every partial specialization—like every full specialization—is associated with the primary template. When a template is used, the primary template is always
