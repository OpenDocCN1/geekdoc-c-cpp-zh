Once we have defined a generic class (template class), we can create a specific instance of this class using the following syntax:

```
class-name<type> obj;
```

Here, **type** is the type of the data that the class will be operating upon. The **class-name<type>** declaration determines the type of object that will be instantiated.

Member functions of a generic class are themselves automatically generic. We do not need to use function templates to explicitly specify them as in a class declaration.

In the following program, a stack template class is declared:

```
#include <iostream>
using namespace std;

const SIZE = 10;

// Declare a stack template class
template <class Ttype>
class Stack {
    Ttype my_stack[SIZE]; // the stack
    int num_el; // number of elements in the stack
public:
    Stack() : num_el = 0; } // constructor
    void push(Ttype obj); // push object on stack
    Ttype pop(); // pop object off stack
}

// Push function
template <class Ttype>
void Stack<Ttype>::push(Ttype obj) {
    if (num_el == SIZE) {
        cout << "Stack is full.\n";
        return;
    }
    my_stack[num_el] = obj;
    num_el++;
}

// Pop function
template <class Ttype>
Ttype Stack<Ttype>::pop() {
```