
```cpp
template<typename T>
class Base {
public:
    void bar();
};

template<typename T>
class Derived : Base<T> {
public:
    void foo() {
        bar(); // calls external bar() or error
    }
};
```

In this example, for resolving the symbol `bar` inside `foo()`, `bar()` defined in `Base` is *never* considered. Therefore, either you have an error, or another `bar()` (such as a global `bar()`) is called.

We discuss this issue in Section 13.4.2 on page 237 in detail. For the moment, as a rule of thumb, we recommend that you always qualify any symbol that is declared in a base that is somehow dependent on a template parameter with `this->` or `Base<T>::`.

## 5.4 Templates for Raw Arrays and String Literals

When passing raw arrays or string literals to templates, some care has to be taken. First, if the template parameters are declared as references, the arguments don’t decay. That is, a passed argument of `"hello"` has type `char const[6]`. This can become a problem if raw arrays or string arguments of different length are passed because the types differ. Only when passing the argument by value, the types decay, so that string literals are converted to type `char const*`. This is discussed in detail in Chapter 7.

Note that you can also provide templates that specifically deal with raw arrays or string literals. For example:

`basics/lessarray.hpp`

```cpp
template<typename T,
         int N,
         int M> bool less (T(&a)[N], T(&b)[M])
{
    for (int i = 0; i<N && i<M; ++i)
    {
        if (a[i]<b[i]) return true; if (b[i]<a[i]) return false;
    }
    return N < M;
}
```

Here, when calling

```cpp
int x[] = {1, 2, 3};
int y[] = {1, 2, 3, 4, 5};
std::cout << less(x,y) << '\n';
```

`less<>()` is instantiated with `T` being `int`, `N` being 3, and `M` being 5.

You can also use this template for string literals:

```cpp
std::cout << less("ab","abc") << '\n';
```

In this case, `less<>()` is instantiated with `T` being `char const`, `N` being 3, and `M` being 4.

If you only want to provide a function template for string literals (and other char arrays), you can do this as follows:

`basics/lessstring.hpp`

```cpp
template<int N, int M>
bool less (char const(&a)[N], char const(&b)[M])
{
    for (int i = 0; i<N && i<M; ++i) {
        if (a[i]<b[i]) return true;
        if (b[i]<a[i]) return false;
    }
    return N < M;
}
```

Note that you can and sometimes have to overload or partially specialize for arrays of unknown bounds. The following program illustrates all possible overloads for arrays:

`basics/arrays.hpp`

```cpp
#include <iostream>

template<typename T>
struct MyClass; // primary template

template<typename T, std::size_t SZ>
struct MyClass<T[SZ]> // partial specialization for arrays of known bounds
{
    static void print() { std::cout << "print() for T[" << SZ << "]\n"; }
};

template<typename T, std::size_t SZ>
struct MyClass<T(&)[SZ]> // partial spec. for references to arrays of known bounds
{
    static void print() { std::cout << "print() for T(&)[" << SZ << "]\n"; }
};

template<typename T>
struct MyClass<T[]> // partial specialization for arrays of unknown bounds
{
    static void print() { std::cout << "print() for T[]\n"; }
};

template<typename T>
struct MyClass<T(&)[]> // partial spec. for references to arrays of unknown bounds
{
    static void print() { std::cout << "print() for T(&)[]\n"; }
};

template<typename T>
struct MyClass<T*> // partial specialization for pointers
{
    static void print() { std::cout << "print() for T*\n"; }
};
```

Here, the class template `MyClass<>` is specialized for various types: arrays of known and unknown bound, references to arrays of known and unknown bounds, and pointers. Each case is different and can occur when using arrays:

`basics/arrays.cpp`

```cpp
#include "arrays.hpp"

template<typename T1, typename T2, typename T3>
void foo(int a1[7], int a2[], // pointers by language rules
         int (&a3)[42], // reference to array of known bound
         int (&x0)[], // reference to array of unknown bound
         T1 x1, // passing by value decays
         T2& x2, T3&& x3) // passing by reference
{
    MyClass<decltype(a1)>::print(); // uses MyClass<T*>
    MyClass<decltype(a2)>::print(); // uses MyClass<T*>
    MyClass<decltype(a3)>::print(); // uses MyClass<T(&)[SZ]>
    MyClass<decltype(x0)>::print(); // uses MyClass<T(&)[]>
    MyClass<decltype(x1)>::print(); // uses MyClass<T*>
    MyClass<decltype(x2)>::print(); // uses MyClass<T(&)[]>
    MyClass<decltype(x3)>::print(); // uses MyClass<T(&)[]>
}

int main()
{
    int a[42];
    MyClass<decltype(a)>::print(); // uses MyClass<T[SZ]>

    extern int x[]; // forward declare array
    MyClass<decltype(x)>::print(); // uses MyClass<T[]>

    foo(a, a, a, x, x, x, x);
}

int x[] = {0, 8, 15}; // define forward-declared array
```

Note that a *call parameter* declared as an array (with or without length) by language rules really has a pointer type. Note also that templates for arrays of unknown bounds can be used for an incomplete type such as `extern int i[]`; and when this is passed by reference, it becomes an `int (&)[]`, which can also be used as a template parameter.²

See Section 19.3.1 on page 401 for another example using the different array types in generic code.

## 5.5 Member Templates

Class members can also be templates. This is possible for both nested classes and member functions. The application and advantage of this ability can again be demonstrated with the `Stack<>` class template. Normally you can assign stacks to each other only when they have the same type, which implies that the elements have the same type. However, you can’t assign a stack with elements of any other type, even if there is an implicit type conversion for the element types defined:

```cpp
Stack<int> intStack1, intStack2; // stacks for ints
Stack<float> floatStack; // stack for floats
...
intStack1 = intStack2; // OK: stacks have same type
floatStack = intStack1; // ERROR: stacks have different types
```

The default assignment operator requires that both sides of the assignment operator have the same type, which is not the case if stacks have different element types.

By defining an assignment operator as a template, however, you can enable the assignment of stacks with elements for which an appropriate type conversion is defined. To do this you have to declare `Stack<>` as follows:

`basics/stack5decl.hpp`

```cpp
template<typename T>
class Stack {
private:
    std::deque<T> elems; // elements

public:
    void push(T const&); // push element
    void pop(); // pop element
    T const& top() const; // return top element
    bool empty() const { // return whether the stack is empty
        return elems.empty();
    }

    // assign stack of elements of type T2
    template<typename T2>
    Stack& operator= (Stack<T2> const&);
};
```

The following two changes have been made:

1. We added a declaration of an assignment operator for stacks of elements of another type T2.
2. The stack now uses a `std::deque<>` as an internal container for the elements. Again, this is a consequence of the implementation of the new assignment operator.

The implementation of the new assignment operator looks like this:³

`basics/stack5assign.hpp`

```cpp
template<typename T>
template<typename T2>
Stack<T>& Stack<T>::operator= (Stack<T2> const& op2)
{
    Stack<T2> tmp(op2); // create a copy of the assigned stack

    elems.clear(); // remove existing elements
    while (!tmp.empty()) { // copy all elements
        elems.push_front(tmp.top());
        tmp.pop();
    }
    return *this;
}
```

First let’s look at the syntax to define a member template. Inside the template with template parameter T, an inner template with template parameter T2 is defined:

```cpp
template<typename T>
template<typename T2>
...
```

Inside the member function, you may expect simply to access all necessary data for the assigned stack op2. However, this stack has a different type (if you instantiate a class template for two different argument types, you get two different class types), so you are restricted to using the public interface. It follows that the only way to access the elements is by calling `top()`. However, each element has to become a top element, then. Thus, a copy of op2 must first be made, so that the elements are taken from that copy by calling `pop()`. Because `top()` returns the last element pushed onto the stack, we might prefer to use a container that supports the insertion of elements at the other end of the collection. For this reason, we use a `std::deque<>`, which provides `push_front()` to put an element on the other side of the collection.

To get access to all the members of op2 you can declare that all other stack instances are friends:

`basics/stack6decl.hpp`

```cpp
template<typename T>
class Stack {
private:
    std::deque<T> elems; // elements
public:
    void push(T const&); // push element
    void pop(); // pop element
    T const& top() const; // return top element
    bool empty() const { // return whether the stack is empty
        return elems.empty();
    }

    // assign stack of elements of type T2
    template<typename T2>
    Stack& operator= (Stack<T2> const&);
    // to get access to private members of Stack<T2> for any type T2:
    template<typename> friend class Stack;
};
```
