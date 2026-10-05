# 18 • Operator Overloading 589

```
Product& ::operator+(const Product& p)
{
    prc += p.prc;
    return *this;
}
```

**Comments:** First, let's find the declaration of sum(). In main() we see that sum() returns both int and Product types. So, we understand that its return type must be generic (e.g., T). The argument in sum() calls vector of int and Product types. Therefore, the type of the vector elements must be generic, the same as the return type T. As we know, for better performance, we use a reference, which we make const so that its elements cannot be modified. Then, we come to the declaration of sum(). Let's see its definition. We understand that the type of the variable must be generic and we initialize it with 0, in order to calculate the correct sum(). ends with the return of t.

Let's decode the definition of the Product class. From the statement cout << p.prc; we understand that the prc member is public. I declare the private; I could also make it public. From the initialization of v we need to add a constructor. We set default zero values, which are needed (basically, prec must be set to 0 when the object is created in sum()). Specifically, when sum(v,p) is called, T will be replaced by Product and the object t will be calculated. When to the calculation of the sum. Okay, when T is int there is no problem, the sum of integers will be calculated. But, when T is Product how will the addition be done we need to overload the operator and add the prc members to calculate their sum. The operator+ function returns the t object and each addition in the for loop stores the current in t.prc.

**C.18.8** Consider the following classes Product and Employee:

```
class Product {
    private:
        int code;
        float prc; // Price.
    public:
        ...
}

class Employee {
    private:
        string name;
        float sal; // Salary.
    public:
        ...
}
```

Define the template function sort() that takes as parameter a vector object (e.g., v), which contains either Product or Employee elements and sorts them. If it contains Product elements, the sorting should be done in increase order. If it contains Employee elements, the sorting should be done in name alphabetical order. To sort the elements each class should contain an inline constructor, an inline function named show() to display the values of its members, and the necessary function to compare the elements of v. Write a program that declares two vector objects with Product and Employee elements, calls sort() and displays their elements.

```
#include <iostream>
#include <string>
#include <vector>
```