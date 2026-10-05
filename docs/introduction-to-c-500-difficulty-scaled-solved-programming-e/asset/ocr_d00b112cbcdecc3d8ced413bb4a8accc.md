# 760 Introduction to C++

```
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

Let's see what happens when they are called. Because f() does not take a parameter from which the compiler will deduce the intended specialization (int or float), we should indicate the type in <>. Thus, when f<int>() is called, T is replaced with int and one object of the A<int> class and one of the A<float> class are created, the value of A<int>::cnt becomes 2 and the value of A<float>::cnt becomes 1. When g(a1) is called, the compiler checks the type of the argument to deduce the specialization. For example, with g(a1), the compiler finds that the type of the argument is A<int> and the program displays the value of al.p.

# Function Template Non-Bound to Class Template

In the previous section we saw that each instantiation of the class is bound to a matching version of the friend function. For example, an int version of the A class is bound to an int version of the friend function. If we declare the template inside the class, we can create non-bound friend functions, that is, every instantiation becomes bound to all versions of the class not just a particular instance as before. For non-bound friends, we use the different names in its parameter-types from the names of the parameter-types of the class. Consider the following program:

```
#include <iostream> // Example 23.12
```

```
template <typename T> class A
private:
    T p;
```