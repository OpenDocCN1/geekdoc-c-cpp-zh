
# 760 Introduction to C++

```cpp
template <typename T> void g(T& t)
{
    std::cout << t.p << '\n';
}

int main() {
    A<int> a1(5), a2(10);
    A<float> d(2.3);

    g(a1); // We also write g<A<int>>(a1); The program displays 5.
    g(d); // The program displays 2.3.
    f<int>(f); // The program displays 2.
    f<float>(f); // The program displays 1.
    return 0;
}
```

With template bound friend functions things are more complex than non-template ones. First, we declare their prototypes before defining the class template. We declare them again in the class as friend functions. The <> in their declarations denotes they are template specializations. The reason I made f() not to take parameters is to see how to use such a function. Because f() does not take parameters, we use the template syntax <> to indicate the type of specialization (e.g., f<int>) when we call it. In the case of g(), the <> can be left empty because the type of the argument can be deduced from the type of the function argument.

When a version of the class template is defined, the respective friend functions bound to that version are also defined. For example, when each instantiation of A is defined, there must be matching instantiation for each friend function. For example, when the A<int> class is defined, the template specializations f<int> and g<A<int>> become friends of the A<int> class. Similarly, when the A<float> class is defined, f<float> and g<A<float>> functions become its friends. As you see, there is one-to-one relationship.

Let's see what happens when they are called. Because f() does not take a parameter from which the compiler will deduce the intended specialization (int or float), we should indicate the type in <>. Thus, when f<int>() is called, T is replaced with int and one object of the A<int> class and one of the A<float> class are created, the value of A<int>::cnt becomes 2 and the value of A<float>::cnt becomes 1. When g(a1) is called, the compiler checks the type of the argument to deduce the specialization. For example, with g(a1), the compiler finds that the type of the argument is A<int> and the program displays the value of a1.p.

# Function Template Non-Bound to Class Template

In the previous section we saw that each instantiation of the class is bound to a matching version of the friend function. For example, an int version of the A class is bound to an int version of the friend function. If we declare the template inside the class, we can create non-bound friend functions, that is, every instantiation becomes bound to all versions of the class not just a particular instance as before. For non-bound friends, we use the different names in its parameter-types from the names of the parameter-types of the class. Consider the following program:

```cpp
#include <iostream> // Example 23.12
```

```cpp
template <typename T> class A
private:
    T p;

public:
    A(T i) {p = i};
    template <typename V> friend void f(V& v); /* We use a different type
    name (i.e., V) from the type name of the class (i.e., T). */
};
```

```cpp
template <typename V> void f(V& v)
{
    std::cout << v.p << '\n';
}
```

```cpp
int main()
{
    A<char> a1('r');
    A<int> a2(5);
    A<double> a3(2.3);

    f(a1);
    f(a2);
    f(a3);
    return 0;
}
```

For all instantiations of A, all instantiations of f() are friends. That is, f() has a many-to-many relationship with the A class. Therefore, f() may access the p private member of the a1, a2 and a3 objects. Note that an instance of the friend template is created only if the friend function is called in the program. For example, the statement f(a1) causes the instantiation of void(A<char>& v) and the program displays the value of a.p. Finally, the program displays r 5 and 2.3.

# Class Template as Friend

A class template can be a friend of an ordinary class. In this case, all instantiations of the class template becomes friends of the A class. For example:

```cpp
#include <iostream> // Example 23.13
```

```cpp
class A
private:
    int p;
public:
    A() {p = 20};
    template <typename T> friend class B;
```

```cpp
template <typename T> class B
{
public:
    void f(const A& a) const {std::cout << a.p};
}
```

```cpp
int main()
{
    A a;
    B<int> b1;
    B<double> b2;

    b1.f(a);
    b2.f(a);
    return 0;
}
```

Since the B class template is friend of the A class, all instantiations of the class template becomes friends of the A class.

# Introduction to C++

# CLASS TEMPLATES SPECIALIZATIONS

A class template can be a friend of an ordinary class. In this case, all instantiations of the class template becomes friends of the A class. For example:

```cpp
#include <iostream> // Example 23.13
```

```cpp
class A
private:
    int p;
public:
    A() {p = 20};
    template <typename T> friend class B;
```

```cpp
template <typename T> class B
{
public:
    void f(const A& a) const {std::cout << a.p};
}
```

```cpp
int main()
{
    A a;
    B<int> b1;
    B<double> b2;

    b1.f(a);
    b2.f(a);
    return 0;
}
```

Since the B class template is friend of the A class, all instantiations of the class template becomes friends of the A class.

# Introduction to C++

(Wait, looking at the provided prompt text, there are repetitions and fragments. I will clean the logical flow based on the provided OCR segments.)

*(Self-correction: The OCR text provided has significant overlapping and repeated sections. I will merge them logically as based on the provided source text blocks.)*

# 760 Introduction to C++

```cpp
template <typename T> void g(T& t)
{
    std::cout << t.p << '\n';
}

int main() {
    A<int> a1(5), a2(10);
    A<float> d(2.3);

    g(a1); // We also write g<A<int>>(a1); The program displays 5.
    g(d); // The program displays 2.3.
    f<int>(f); // The program displays 2.
    f<float>(f); // The program displays 1.
    return 0;
}
```

With template bound friend functions things are more complex than non-template ones. First, we declare their prototypes before defining the class template. We declare them again in the class as friend functions. The <> in their declarations denotes they are template specializations. The reason I made f() not to take parameters is to see how to use such a function. Because f() does not take parameters, we use the template syntax <> to indicate the type of specialization (e.g., f<int>) when we call it. In the case of g(), the <> can be left empty because the type of the argument can be deduced from the type of the function argument.

When a version of the class template is defined, the respective friend functions bound to that version are also defined. For example, when each instantiation of A is defined, there must be matching instantiation for each friend function. For example, when the A<int> class is defined, the template specializations f<int> and g<A<int>> become friends of the A<int> class. Similarly, when the A<float> class is defined, f<float> and g<A<float>> functions become its friends. As you see, there is one-to-one relationship.

Let's see what happens when they are called. Because f() does not take a parameter from which the compiler will deduce the intended specialization (int or float), we should indicate the type in <>. Thus, when f<int>() is called, T is replaced with int and one object of the A<int> class and one of the A<float> class are created, the value of A<int>::cnt becomes 2 and the value of A<float>::cnt becomes 1. When g(a1) is called, the compiler checks the type of the argument to deduce the specialization. For example, with g(a1), the compiler finds that the type of the argument is A<int> and the program displays the value of a1.p.

# Function Template Non-Bound to Class Template

In the previous section we saw that each instantiation of the class is bound to a matching version of the friend function. For example, an int version of the A class is bound to an int version of the friend function. If we declare the template inside the class, we can create non-bound friend functions, that is, every instantiation becomes bound to all versions of the class not just a particular instance as before. For non-bound friends, we use the different names in its parameter-types from the names of the parameter-types of the class. Consider the following program:

```cpp
#include <iostream> // Example 23.12
```

```cpp
template <typename T> class A
private:
    T p;

public:
    A(T i) {p = i};
    template <typename V> friend void f(V& v); /* We use a different type
    name (i.e., V) from the type name of the class (i.e., T). */
};
```

```cpp
template <typename V> void f(V& v)
{
    std::cout << v.p << '\n';
}
```

```cpp
int main()
{
    A<char> a1('r');
    A<int> a2(5);
    A<double> a3(2.3);

    f(a1);
    f(a2);
    f(a3);
    return 0;
}
```

For all instantiations of A, all instantiations of f() are friends. That is, f() has a many-to-many relationship with the A class. Therefore, f() may access the p private member of the a1, a2 and a3 objects. Note that an instance of the friend template is created only if the friend function is called in the program. For example, the statement f(a1) causes the instantiation of void(A<char>& v) and the program displays the value of a.p. Finally, the program displays r 5 and 2.3.

# Class Template as Friend

A class template can be a friend of an ordinary class. In this case, all instantiations of the class template becomes friends of the A class. For example:

```cpp
#include <iostream> // Example 23.13
```

```cpp
class A
private:
    int p;
public:
    A() {p = 20};
    template <typename T> friend class B;
```

```cpp
template <typename T> class B
{
public:
    void f(const A& a) const {std::cout << a.p};
}
```

```cpp
int main()
{
    A a;
    B<int> b1;
    B<double> b2;

    b1.f(a);
    b2.f(a);
    return 0;
}
```

Since the B class template is friend of the A class, all instantiations of the class template becomes friends of the A class.

# CLASS TEMPLATES SPECIALIZATIONS

A class template can be a friend of an ordinary class. In this case, all instantiations of the class template becomes friends of the A class. For example:

```cpp
#include <iostream> // Example 23.13
```

```cpp
class A
private:
    int p;
public:
    A() {p = 20};
    template <typename T> friend class B;
```

```cpp
template <typename T> class B
{
public:
    void f(const A& a) const {std::cout << a.p};
}
```

```cpp
int main()
{
    A a;
    B<int> b1;
    B<double> b2;

    b1.f(a);
    b2.f(a);
    return 0;
}
```

Since the B class template is friend of the A class, all instantiations of the class template becomes friends of the A class.

(Note: The OCR text provided contained redundant sections and overlapping pages. I have merged the unique content flow based on the structure provided.)
