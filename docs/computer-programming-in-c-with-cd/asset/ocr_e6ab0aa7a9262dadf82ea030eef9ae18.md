(you can find this example in the InlineInClass.cpp file on the CD in the code\chapter6 folder):

# **▶ Listing 6: Creating Inline Functions in a Class**

```
```cpp
#include<iostream.h>

class MyClass
{
    int x,y,z;
public:
    void getdata()
    {
        cout<<"Enter any two numbers";
        cin>>x>>y;
        z=x+y;
    }
    void displayData()
    {
        cout<<"The sum of two numbers is="<<z<<endl;
    }
};

int main()
{
    MyClass o;
    o.getdata();
    o.displayData();
    return 0;
}
```
```

# **Output:**

```
```text
Enter any two numbers78
43
The sum of two numbers is=121
```
```

In Listing 6, getData() and displayData() are two inline member functions of the MyClass class. These functions are defined inside the boundary of the MyClass class without using the inline keyword.

The functions defined outside a class are non-inline or outline functions. Member functions defined outside the class declaration can also be made inline functions by prefixing the `inline` keyword to its definition. Listing 7 shows the creation of inline functions outside a class (you can find this example in the InlineOutClass.cpp file on the CD in the code\chapter6 folder):