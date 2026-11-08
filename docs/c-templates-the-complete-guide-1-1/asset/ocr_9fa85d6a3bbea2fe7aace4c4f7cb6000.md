# Chapter 2

# Class Templates

Similar to functions, classes can also be parameterized with one or more types. Container classes, which are used to manage elements of a certain type, are a typical example of this feature. By using class templates, you can implement such container classes while the element type is still open. In this chapter we use a stack as an example of a class template.

# 2.1 IMPLEMENTATION OF CLASS TEMPLATE STACK

As we did with function templates, we declare and define class Stack in a header file as follows:

[Click here to view code image](#)

`basics/stack1.hpp`

```
```cpp
#include <vector>
#include <cassert>

template<typename T>
class Stack {
private:
    std::vector<T> elems;    // elements

public:
    void push(T const& elem); // push element

    void pop();               // pop element

    T const& top() const;     // return top element

    bool empty() const {      // return whether the stack is empty
        return elems.empty();
    }
};

template<typename T>
void Stack<T>::push (T const& elem)
{
    elems.push_back(elem);   // append copy of passed element
}

template<typename T>
void Stack<T>::pop()
{
    assert(!elems.empty());  // remove last element
    elems.pop_back();
}

template<typename T>
T const& Stack<T>::top() const
{
    assert(!elems.empty());  // remove last element
    return elems.back();     // return last element
}

template<typename T>
T const& Stack<T>::top() const
```
```