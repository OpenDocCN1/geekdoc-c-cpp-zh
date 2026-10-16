means that **re** is initialized to the value of **r** and **im** is initialized to the value of **i**. In other words, the above code has essentially the same meaning as:

```
Complex(double r = 0, double i = 0){
    re = r; im = i;
}
```

The constructor is also defined with default values given for its parameters:

```
Complex(double r = 0, double i = 0)
```

This allows Complex objects to be created with 0, 1, or 2 parameters, and avoids the need to create different overloaded constructors:

```
Complex i(0,1);  // i constructed as (0,1)
Complex x;      // y constructed as default (0,0)
Complex x(1);    // x constructed as (1,0)
```

# 5.4.2 Using a Template Class to Implement a Generic Collection

You saw how a generic collection class is defined in Java in Section 5.3.2. A similar feature, called **template classes**, is used to define generic collections in C++. Although the standard template library (STL) of C++ includes several built-in collection classes, let’s develop a LinkedStack class to see how a C++ template class works.

Our C++ LinkedStack class has the same basic interface as the Java version discussed in Section 5.3.2. Here is a short C++ program that exercises some of its capabilities:

```
#include <iostream>
using std::cout;
using std::endl;
#include "LinkedStack.c"

int main(){
    int number;
    LinkedStack<int> stack;
    for (number = 1; number <= 5; number++)
        stack.push(number);
    cout << "The size is " << stack.size() << endl;
    while (stack.size() != 0)
        cout << stack.pop() << " ";
    cout << endl;
}
```

As you can see, this code declares a stack type in a similar manner to the Java version, although in this case the **int** type can be specified directly as the stack’s element type. However, unlike in Java, a new **LinkedStack** object is automatically created and assigned to the **stack** variable upon the mere mention of that variable in the declaration. Otherwise, the usage of **LinkedStack** is exactly the same as in the Java example.