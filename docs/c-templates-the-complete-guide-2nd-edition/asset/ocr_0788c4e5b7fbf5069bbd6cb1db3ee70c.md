In addition, it is used in push() to check whether the stack is full: Click here to view code image

```
template<typename T, std::size_t Maxsize>
void Stack<T,Maxsize>::push (T const& elem)
{
assert(numElems < Maxsize);
elems[numElems] = elem; // append element ++numElems; // increment number of elements
}
```

To use this class template you have to specify both the element type and the maximum size: Click here to view code image

basics/stacknontype.cpp

```
#include "stacknontype.hpp"
#include <iostream>
#include <string>

int main()
{
Stack<int,20> int20Stack; // stack of up to 20 ints
Stack<int,40> int40Stack; // stack of up to 40 ints
Stack<std::string,40> stringStack; // stack of up to 40 strings

// manipulate stack of up to 20 ints
int20Stack.push(7);
std::cout << int20Stack.top() << '\n';
int20Stack.pop();

// manipulate stack of up to 40 strings
stringStack.push("hello");
std::cout << stringStack.top() << '\n';
stringStack.pop();
}
```

Note that each template instantiation is its own type. Thus, int20Stack and int40Stack are two different types, and no implicit or explicit type conversion between them is defined. Thus, one cannot be used instead of the other, and you cannot assign one to the other.

Again, default arguments for the template parameters can be specified: Click here to view code image

```
template<typename T = int, std::size_t Maxsize = 100>
class Stack {
... 
};
```