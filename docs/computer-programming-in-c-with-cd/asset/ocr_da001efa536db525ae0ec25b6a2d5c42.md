+   - [ ] Creating a friend function as a bridge between two classes
+   - [ ] Creating friend classes

# Defining a Friend Function

Functions that are defined outside a class but can still access the private members of the class are called friend functions. A non-member function cannot access the private data of a class. However, any non-member function may be declared a friend by a class so that the function may directly access the private variables and methods of the class objects. Listing 33 shows how to declare and use a friend function (you can find this example in the SimpleFriend.cpp file on the CD in the code\chapter6 folder):

# ▶ Listing 33: Declaring and Using a Friend Function

```
```cpp
#include<iostream.h>

class Calculate
{
    int x,y;
    public:

    void readData()
    {
        cout<<"Enter any two numbers"<<endl;
        cin>>x>>y;
    }
    friend void add(Calculate c);
};
void add(Calculate cal)
{
    cout<<"The sum of two numbers is:"<<cal.x+cal.y<<endl;
}
int main()
{
    Calculate calc;
    calc.readData();
    add(calc);
    return 0;
}
```
```

**Output:**

```
```text
Enter any two numbers
37
82
The sum of two numbers is:119
```
```