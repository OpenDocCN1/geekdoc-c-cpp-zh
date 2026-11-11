Note that the concept of function overriding must not be confused with the concept of function overloading. These terms look similar, but they do different tasks. Function overloading is to create more than one function with the same name, but with different signatures. Function overriding, on the other hand, is to create a function in a derived class with the same name and signature as a function in the base class.

# TEST YOUR KNOWLEDGE

**Q1.** Create a base class, called Computer, containing functions to display information related to a computer system, such as speed and memory size. Create a derived class, called Laptop, from the Computer base class. The Laptop class must override the functions of the Computer class and also have its own functions.

Ans.

```
```cpp
#include<iostream.h>

class Computer       //base class
{
    float speed;
    int main_memory;
    int harddisk_memory;

public:
    void set_speed(float);
    void set_mmemory(int);
    void set_hmemory(int);
    float get_speed();
    int get_mmemory();
    int get_hmemory();
};

void Computer::set_speed(float sp)
{
    speed=sp;
}
void Computer::set_mmemory(int m)
{
    main_memory=m;
}
void Computer::set_hmemory(int h)
{
    harddisk_memory=h;
}
int Computer::get_hmemory()
{
    return harddisk_memory;
}
int Computer::get_mmemory()
```
```