
# ISO/IEC 14882:2017(E)

such a type may be aliased, e.g., by a typedef-name. — end note

## 17.5 Template declarations

- 1 A template-id, that is, the template-name followed by a template-argument-list shall not be specified in the declaration of a template declaration. [Example:
```cpp
template<class T1, T2> int Class&T1, T2 {}; // error
template<class T1, int> void sort(T1 data[], T1); // error
```
— [example]: However, this is allowed in class template partial specializations (17.5.5). — end note |

- 2 For purposes of name lookup and instantiation, default arguments and noexcept-specifiers of function templates and default arguments and noexcept-specifiers of member functions are considered definitions; each default argument or noexcept-specifier is a separate definition which is unrelated to the function definition or to any other default arguments or noexcept-specifiers; the substatements of a constexpr (9.4.1) are considered definitions.

- 3 Because an alias-declaration cannot declare a template-id, it is not possible to partially or explicitly specialize an alias.

## 17.5.1 Class templates

- 1 A class template defines the layout and operations for an unbounded set of related types.
[Example]: A single class template List might provide an unbounded set of classes: List<T> for every type T, each describing a list of elements of type T. Similarly, a class template Array describing a contiguous, dynamic array might be defined like this:
```cpp
template<class T>
Array {
T* v;
int sz;
public:
    explicit Array(int);
    T& operator[](int i) { return v[i]; }
};
```
The prefix template<class T> specifies that a template is being declared and that a type-name T is used in the declaration. In other words, Array is a parameterized type with T as its parameter. — end example |

- 3 When a member function, a member class, a member enumeration, a static data member or a member of a class template is defined outside of the class template, the member definition is defined as a template definition in which the template-parameters are those of the class template. The names of the template parameters used in the definition of the member may be different from the template parameter names used in the class template. The template argument list following the class template name in the member definition matches the parameters in the same order as the one used in the template argument list. [Example]:
```cpp
template<class T1, class T2> struct A {
void f1();
void f2();
};

template<class T2, class T1> void A<T2, T1>::f1() {} // OK
template<class T2, class T1> void A<T1, T2>::f2() {} // error
```
```cpp
template<class ... Types> struct B {
void f3();
void f4();
};
```
```cpp
template<class ... Types> void B<Types..>::f3() {} // OK
template<class ... Types> void B<Types..>::f4() {} // error
// end example];
```

- 4 In a redeclaration, partial specialization, explicit specialization or explicit instantiation of a class template, the key-class shall agree in kind with the original class template declaration (10.1.7.3).

## 17.5.1.1 Member functions of class templates [temp.mem.func]

- 1 A member function of a class template may be defined outside of the class definition in which it is declared. [Example]:
```cpp
template<class T> class Array {
T* v;
int sz;
public:
explicit Array(int);
T operator[](int);
T elem(int i) { return v[i]; };
};
```
declares three functions. The subscript function might be defined like:
```cpp
template<class T> T Array<T>::operator[](int i) {
if (i < 0 || i >= sz) throw error("Array error");
return v[i];
}
// end example];
```

- 2 The template-arguments for a member function of a class template are determined by the template-arguments of the type of the object for which the member function is called. [Example: The template-argument for Array<>::operator() will be determined by the Array to which the subscripting is applied.
```cpp
Array<int> v1(20);
Array<complex> v2(30);
```
```cpp
v1[3] = {}; // Array<int>::operator()
v2[3] = complex(7,8); // Array<complex>::operator()
// end example];
```

## 17.5.1.2 Member functions of class templates [temp.mem.class]

- 1 A member function of a class template may be defined outside of the class definition in which it is declared. [Note: The member class must be defined before its first use that requires an instantiation (17.7.1). For example:
```cpp
template<class T> struct A {
class B;
};
nA<int>::B b1; // requires A to be defined but not A::B
template<class T> class A<T>:B { };
nA<int>::B b2; // requires A::B to be defined
// end note];

## 17.5.1.3 Static data members of class templates

A definition for a static data member or static data member template may be provided in a namespace enclosing the definition of the static member's class template. [Example:
```cpp
template<class T> class X {
    static T s;
};
template<class T> X>::s = 0;
struct limits {
    template<class T>
    static const T min;
};
template<class T>
    const T limits::min = {};
// end example
```

- 2 An explicit specialization of a static data member declared as an array of unknown bound can have a different bound from its definition, if any. [Example:
```cpp
template<class T> struct A {
    static int i[];
};
template<class T> int A<T>::i = {}; // corrected from original OCR
```
```cpp
template<class T> struct A {
    static int i[];
};
// 1 element
// end example
```

## 17.5.1.4 Enumeration members of class templates

An enumeration member of a class template may be defined outside the class template. [Example:
```cpp
template<class T> struct A {
    enum E;
};
template<class T> enum A<T>::E { value };
// end example
```

## 17.5.2 Member templates

- 1 A template can be declared within a class; such a template is a member template. A member template can be defined within or outside its class definition shall be specified with the template-parameters of the class template. [Example:
```cpp
template<class T> struct string {
    template <class T2> int compare(const T2&);
};
template<class T> template <class T2> int string<T>::compare(const T2&) const {
// end example
```

- 2 A local class of non-closure type shall not have member templates. Access control rules (Clause 14) apply to member templates. A destructor shall not be a member. A non-template member function (11.3.5) with a given name and a member template function of the same name, both could be used to generate a specialization of the same type, both be be declared in a class. [Example:
```cpp
template <class T> struct A {
    void f(int);
    template <class T2> void f(T2);
};

template <class> void A<T>::f(int) // non-template member
template <class> template <T> void A<T>::f(int) // member template specialization

int main() {
    A<char> ac;
    ac.f(1);    // non-template
    ac.f('c');  // template
    ac.f(1);    // template
}
// end example
```

- 3 A member function template shall not be virtual. [Example:
```cpp
template <class T> struct AA {
    template <class O> virtual void g(C); // error
    virtual void f();                   // OK
};
// end example
```
class D : public B {
    template <class T> void f(T); // does not override B::f(int)
    void f(int i) {f(i); } // overriding function that calls the template instantiation
};
// end example
```

- 4 A specialization of a member function template does not override a virtual function from a base class. [Example:
```cpp
struct A {
    template <class T> operator T*();
};
template <class T> A::operator T*() { return 0; }
template <> A::operator char*() { return 0; } // specialization
template <> A::operator void*() {} // explicit instantiation

int main() {
    A a;
    int* ip;
}
```
```

- 5 A specialization of a conversion function template is referenced in the same way as a non-template conversion that converts to the same type. [Example:
