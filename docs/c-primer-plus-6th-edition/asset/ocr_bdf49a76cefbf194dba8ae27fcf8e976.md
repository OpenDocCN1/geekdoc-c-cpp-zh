# C++11 Features Revisited

```
char c1 = {66}; // int-to-char, in, allowed
double c2 = {66}; // int-to-double, allowed
```

# std::initializer_list

C++11 provides an initializer_list template class (discussed in Chapter 16, "The String Class and the Standard Template Library") that can be used as a constructor argument.If a class has a constructor, the brace syntax can be used only with that constructor.Items in the list should all be of the same type or be convertible to the same type.The STL provide constructors with initializer_list arguments:

```
vector<int> a1(10); // uninitialized vector with 10 elements
vector<int> a2(10); // initializer-list, a2 has 1 element set to 10
vector<int> a3(4,6,1); // 3 elements set to 4,6,1
```

The initializer_list header file provides support for this template class.The class begin() and end() member functions specify the range of the list.You can use an initializer_list argument for regular functions as well as for constructors:

```
#include <initializer_list>
double sum(std::initializer_list<double> il);
int main()
{
    double total = sum({2.5,3.1,4}); // 4 converted to 4.0
}
{
    double tot = 0;
    for (auto p = il.begin(); p!=il.end(); p++)
        tot += *p;
    return tot;
}
```

# Declarations

C++11 implements several features that simplify declarations, particularly for situations arising when templates are used.

# auto

C++11 strips the keyword auto of its former meaning as a storage class specifier(Chapter 9,"Memory Models and Namespaces") and puts it to use (Chapter 3) to implement-automatic type deduction, provided that an explicit initializer is given.The compiler sets the type of the variable to the type of the initialization value:

```
auto mason = 112; // mason is type int
auto pt = &mat; // pt is type int *
double fm=(double, int);
auto pf = fm; // pf is type double (*) (double,int)
```