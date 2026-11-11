```
```cpp
{
public:
    void sound() { cout << "winnie"<<endl; }
};

class Pig : public Mammal
{
public:
    void sound() { cout << "oink"<<endl; }
};

int main()
{
    Mammal* ptr1[5];
    Mammal* ptr2;
    ptr2 = new Dog;
    ptr1[0] = ptr2;
    ptr2 = new Cat;
    ptr1[1] = ptr2;
    ptr2 = new Horse;
    ptr1[2] = ptr2;
    ptr2 = new Pig;
    ptr1[3] = ptr2;
    ptr2 = new Mammal;
    ptr1[4] = ptr2;
    for (int i=0;i<5;i++)
        ptr1[i]->sound();
    return 0;
}
```
```

Ans. The output of the preceding program is as follows:

```
```text
woof
Meow
winnie
oink
Mammal sound....
```
```

# Q10. What is the output of the following program?

```
```cpp
#include <iostream.h>

class Vehicle {
protected:
    int i, j;
public:
    void set1(int a, int b) {
        i = a;
        j = b;
```
```