```
```cpp
}

// nothing else to do
}

template<typename T, std::size_t Maxsize>
void Stack<T,Maxsize>::push (const T& elem)
{
    assert(numElems < Maxsize);
    elems[numElems] = elem;    // append element
    ++numElems;                // increment number of elements
}

template<typename T, std::size_t Maxsize>
void Stack<T,Maxsize>::pop()
{
    assert(!elems.empty());
    --numElems;                // decrement number of elements
}

template<typename T, std::size_t Maxsize>
const T& Stack<T,Maxsize>::top () const
{
    assert(!elems.empty());
    return elems[numElems-1];  // return last element
}
```
```

The new second template parameter, Maxsize, is of type int. It specifies the size of the internal array of stack elements.

**Click here to view code image**

```
```cpp
template<typename T, std::size_t Maxsize>
class Stack {
private:
    T elems[Maxsize];       // elements
    int numElems;
};
```
```

In addition, it is used in push() to check whether the stack is full:

**Click here to view code image**

```
```cpp
template<typename T, std::size_t Maxsize>
void Stack<T, Maxsize>::push (const T& elem)
{
    if (numElems == Maxsize) {
        throw std::out_of_range("Stack<>::push(): stack full");
    }
    elems[numElems] = elem;    // append element
    ++numElems;                // increment number of elements
}
```
```

To use this class template you have to specify both the element type and the maximum size:

**Click here to view code image**

basics/stackontype.cpp

```
```cpp
#include "Stackontype.hpp"
#include <iostream>
#include <string>

int main()
{
    Stack<int,20>       intStack;       // stack of ints
    Stack<float,40>     floatStack;     // stack of floats
    Stack<std::string,40> stringStack;  // stack of strings

    // manipulate stack of up to 20 ints
```
```