
```text
hiding.cpp: In function ‘void h(D*)’:
hiding.cpp:13:12: error: invalid conversion from
‘int’ to ‘const char*’ [-fpermissive]
        pd->f(1);
             ^

hiding.cpp:8:9: error: initializing argument 1
of ‘int D::f(const char*)’ [-fpermissive]
        int f(const char*);
            ^
```

A function member of a derived class is not in the same scope as a function member of the same name in a base class. Here `D::f(const char*)` hides `B::f(int)` rather than overloading it.

Hence the call `pd->f(1)` is an error.

### Question 205: Hiding operators

Review the program.

**Program 13.19: hiding operators**

```cpp
1  struct A { };
3  void operator + (A, A);
5  struct B
6  {
7      void operator + (B);
8      void f();
9  };
11 A a;
13 void B::f()
14 {
15     operator+ (a,a);
16     a + a;
17 }
```

### Solution of Question 205

Compiler error is:

```text
operators.cpp:15:18: error: too many arguments to
function call, expected 1,
        have 2
        operator+ (a,a);
~~~~~~~~~~        ^
operators.cpp:7:5: note: 'operator+' declared here
    void operator + (B);

1 error generated.
```

The lookup rules for operators in expressions are different than the lookup rules for operator function names in a function call.

Here `operator+ (a,a)` is in error because global operator is hidden by the member operator. When the expression `a + a` is OK as it calls the global `operator+`.

## Chapter 14: Templates

### Question 206: Non-type template parameters

Which of the following class template declarations is valid?

```cpp
1 template<double d> class X;
2 template<double* pd> class Y;
3 template<double& rd> class Z;
```

### Solution of Question 206

A non-type template-parameter cannot be declared to have floating point, class, or void type.
Hence `template<double d> class X` is invalid, the rest are OK.

### Question 207: Default template parameters

Review the program.

```cpp
1 template<class T1, class T2 = int> class A;
2 template<class T1 = int, class T2> class A;
```

### Solution of Question 207

The set of default template-arguments available for use with a template declaration or definition is obtained by merging the default arguments from the definition (if in scope) and all declarations in scope in the same way default function arguments are.
Hence the program is equivalent to

```cpp
1 template<class T1 = int, class T2 = int> class A;
```

### Question 208: Template and template-id

Review the program.

```cpp
1 template <class T>
2 struct A
3 {
4     void f(int);
5     template <class U>
6     void f(U);
7 };
8
9 template <class T>
10 void f(T t)
11 {
12     A<T> a;
13     a.template f<>(t);
14     a.template f(t);
15 }
16
17 template <class T>
18 struct B
19 {
20     template <class T2>
21     struct C { };
22 };
23
24 template <class T, template <class X> class TT = T::template C>
25 struct D { };
26
27 D<B<int> > db;
```

### Solution of Question 208

`a.template f<>();` is OK: it calls the template, but `a.template f();` is in error because it is not a template-id. The default template parameter of `struct D` is also OK because `T::template C` names a class template.

### Question 209: Template argument and type-id

What is the output of the program?

**Program 14.1: template argument and type-id**

```cpp
1 #include <iostream>
3 template<class T>
4 void f()
5 {
6     std::cout << "template<class T> void f" << std::endl;
7 }
8
9 template<int I>
10 void f()
11 {
12     std::cout << "template<int I> void f" << std::endl;
13 }
14
15 int main()
16 {
17     f<int>();
18 }
```

### Solution of Question 209

It prints

```cpp
template<class T> void f
```

In a template-argument, an ambiguity between a type-id and an expression is resolved to a type-id, regardless of the form of the corresponding template-parameter.
Hence `f<int>()` calls the first `f()` because `int()` is a type-id.

### Question 210: Explicit specialization vs static

Is this program valid?

```cpp
template <class T> struct A
{
    static int i[];
};

template <class T> int A<T>::i[4];
template <> int A<int>::i[] = { 1 };
```

### Solution of Question 210

Yes.

An explicit specialization of a static data member declared as an array of unknown bound can have a different bound from its definition, if any.

### Question 211: Virtual member function template

Review the program.

**Program 14.2: virtual member function template**

```cpp
template <class T>
struct A
{
    template <class U>
    virtual void f(U);
};
```

### Solution of Question 211

Compiler error is:

```text
virtual_template.cpp:5:5: error:
'virtual' cannot be specified on member
    function templates
    virtual void f(U);
    ~~~~~~~
1 error generated.
```

A member function template cannot be virtual.

### Question 212: Override virtual and template

Which of the following member function overrides `B::f(int)`?

```cpp
class B
{
    virtual void f(int);
};
class D : public B
{
    template <class T>
    void f(T);
    void f(int i)
    {
        f<>(i);
    }
};
```

### Solution of Question 212

A specialization of a member function template does not override a virtual function from a base class. Hence `template <class T> void f(T)` does not override `B::f(int)`. `void f(int i)` is the overriding function that calls the template instantiation.

### Question 213: Parameter pack

What is a template parameter pack and function parameter pack?

### Solution of Question 213

A template parameter pack is a template parameter that accepts zero or more template arguments. For example:

```cpp
template<class ... Types> struct Tuple { };
Tuple<> t0;                  // Types contains no arguments
Tuple<int> t1;               // Types contains one argument : int
Tuple<int, float> t2;        // Types contains two arguments : int and float
Tuple<> error;               // error : <> is not a type
```

A function parameter pack is a function parameter that accepts zero or more function arguments. For example:

```cpp
1 template<class ... Types> void f(Types ... args);
2 f(); // args contains no arguments
3 f(1); // args contains one argument: int
4 f(2, 1.0); // args contains two arguments: int and double
```

### Question 214: Alias template

What is an alias template?

### Solution of Question 214

A template-declaration in which the declaration is an alias-declaration declares the identifier to be an alias template. An alias template is a name for a family of types. The name of the alias template is a template-name.

When a template-id refers to the specialization of an alias template, it is equivalent to the associated type obtained by substitution of its template-arguments for the template-parameters in the type-id of the alias template.

For example:

```cpp
1 template<class T> struct Alloc { /* ... */ };
2 template<class T> using Vec = vector<T, Alloc<T>>;
3 Vec<int> v; // same as vector<int, Alloc<int>> v;
```

Please note that an alias template name is never deduced.

## Chapter 15: Standard Library

### Question 215: Constraint class

Write a constraint class `HasEqual` that checks for the existence of the `==` operator.

### Solution of Question 215

```cpp
template<typename T, typename U>
struct HasEqual
{
    HasEqual() { auto p = constraints; }

    static void constraints(T x, U y)
    {
        x == y;
    }
};
```

The `HasEqual` constructor forces the instantiation of the static constraints member function by declaring a pointer to the function. This function implements a set of valid expressions for the objects introduced by its formal parameters.

The body of this constraints function contains a single statement that looks for a lookup on an appropriate `==` for types of `T` and `U`. If no such operator can be found, instantiation will fail, and the compiler emits the appropriate error message.

The result of the expression is unconstrained here.

### Question 216: Reusing constraint class

Reuse the above constraint class `HasEqual` to implement the concept class `EqualityComparable`.

### Solution of Question 216

Constraint classes can be reused through either inheritance or composition.
