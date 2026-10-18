```
```cpp
Info *p;
Name n;
p = n;
p->getInfo();
}
/*
```
```

# 9.2 Identify the error in the following program.

```
```cpp
#include <iostream.h>
class Person
{
    int age;
public:
    Person()
    {
    }
    Person(int age)
    {
        this.age = age;
    }
    Person& operator < (Person &p)
    {
        return age < p.age ? p: *this;
    }
    int getAge()
    {
        return age;
    }
};
Void main ()
{
    Person P1 (15);
    Person P2 (11);
    Person P3;
    //if p1 is less than p2
```
```