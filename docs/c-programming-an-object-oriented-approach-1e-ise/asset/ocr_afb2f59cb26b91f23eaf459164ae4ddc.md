# **Program 19.22** Using `for_each` with a user-defined function (Continued)

```
```cpp
#include <iostream>
using namespace std;

// Definition of the print function
void print(int value)
{
    cout << value << " ";
}

int main()
{
    // Instantiation of a vector object and storing three values
    vector<int> vec;
    vec.push_back(24);
    vec.push_back(42);
    vec.push_back(73);
    // Using a print function to print the value of each element
    for_each(vec.begin(), vec.end(), print);
    return 0;
}

Run:
24  42  73
```
```

be a pointer to a function. We pass the name *print* and then we define a function named *print* with one argument. The print function takes the value of its argument from the iterator (*\*iterator*).

# 19.6.2 Function Objects (Functors)

In Chapter 13 we learned that we can overload the *function operator*, a pair of parentheses, to create a *function object* (sometimes called a *functor*). Figure 19.15 shows how we write a regular function and a function object.

Program 19.23 shows how we can call a *functor* from another function (*main*). We create a class named *Print*, overload the *operator()*, create an object of the class, and call the operator. Note that calling the overloaded operator is simply calling the object instantiated from the class and inserting the arguments inside the parentheses. In fact, we are calling *print.operator()(45)* in line 16.

![](bbox=[0.331, 0.795, 0.749, 0.907])

**Figure 19.15** A regular function versus a function object