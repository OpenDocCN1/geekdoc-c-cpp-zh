# 572 Introduction to C++

```
a = (r1 == r2); // Equivalent to a = (r1.operator==(r2));
if(a == 1)
    std::cout << "Both are the same\n";
else if (a == 2)
    std::cout << "One is the same\n";
else
    std::cout << "Unequal\n";
    return 0;
```

As we learned, the expression (r1 == r2) does not perform the typical comparison, but it invokes the operator== function of the r1 object with argument the r2 object. Then we can test its return value as we do with any function. The parentheses are not necessary; I just added them to make clear that the function will be executed first.

One more, find the errors in the following program.

```
#include <iostream>

class A
{
public:
    int t;
    A(int i) { t = i; }
    void operator+(int i) { t += i; }
};

class B
{
public:
    int t;
    B(int i) { t = i; }
};

int main()
{
    A a1(10), a2;
    B b1(a1.t);

    a2 = a1+5;
    a1+5;
    b1+5;
    5+a1;
    return 0;
}
```

Since a non-default constructor is defined in A, the declaration of a2 is wrong, no default constructor is defined. The declaration b1(a1.t) is wrong, because the access to the private member t is not allowed. The private label is needed, since the class members are private by default. The statement a2 = a1+5 is not acceptable, because the overloaded function of + operator returns nothing. The statement a1+5 is acceptable and adds 5 to the member t of the a1 object. The statement b1+5 is not acceptable, because overloaded function of + is defined in class B. Finally, the statement 5+a1 is not acceptable, because an object must be at the left of the operator. To better understand, 5+a1; is translated to 5.operator(a1); which is not an acceptable expression. We'll see how to handle this situation in the next section.