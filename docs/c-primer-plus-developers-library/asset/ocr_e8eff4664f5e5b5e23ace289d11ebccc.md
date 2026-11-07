This allows you to use the `{}` syntax with the `Position(int,int,int)` constructor:

```
Position A = {20, -3};  // uses Position(20, -3, 0)
```

# Using `initializer_list`

You can use `initializer_list` objects in your code by including the `initializer_list` header file. The template class has `begin()` and `end()` members, and you can use them to access list elements. It also has a `size()` member that returns the number of elements. Listing 16.22 shows a simple example using `initializer_list`. It requires a compiler that supports this C++11 feature.

Listing 16.22  **list.cpp**

```
```cpp
// list.cpp -- use initializer_list (C++11 feature)
#include <iostream>
#include <initializer_list>

double sum(std::initializer_list<double> il);
double average(const std::initializer_list<double> & ril);

int main()
{
    using std::cout;

    cout << "List 1: sum = " << sum({2,3,4})
         << ", ave = " << average({2,3,4}) << '\n';
    std::initializer_list<double> dl = {1.2, 2.2, 3.3, 4.4, 5.5};
    cout << "List 2: sum = " << sum(dl)
         << ", ave = " << average(dl) << '\n';
    dl = {16.0, 25.0, 36.0, 40.0, 64.0};
    cout << "List 3: sum = " << sum(dl)
         << ", ave = " << average(dl) << '\n';
    return 0;
}

double sum(std::initializer_list<double> il)
{
    double tot = 0;
    for (auto p = il.begin(); p != il.end(); p++)
        tot += *p;
    return tot;
}

double average(const std::initializer_list<double> & ril)
{
    double tot = 0;
```
```