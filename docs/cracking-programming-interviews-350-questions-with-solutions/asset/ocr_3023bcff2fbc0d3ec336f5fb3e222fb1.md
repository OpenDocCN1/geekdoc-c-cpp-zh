# Program 8.38: injected class name

```
```cpp
#include <iostream>
struct A
{
    A()
    {
        std::cout << "::A()" << std::endl;
    }
    ~A()
    {
        std::cout << "::~A()" << std::endl;
    }
};
struct B
{
    struct A
    {
        A()
        {
            std::cout << "B::A()" << std::endl;
        }
        ~A()
        {
            std::cout << "B::~A()" << std::endl;
        }
    };
    void f(::A* a);
};
void B::f(::A* a)
{
    a->~A();
}
int main()
{
    B().f(new A);
}
```
```

# Solution of Question 37

The output is:

```
```
::A()
::~A()
```
```