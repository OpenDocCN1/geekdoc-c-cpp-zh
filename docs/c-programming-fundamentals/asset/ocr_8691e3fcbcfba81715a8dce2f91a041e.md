+   c. It is a technique to avoid the multiple inheritances of the classes.
+   
+   d. It is a technique to avoid creating multiple copies of the base class code for the derived or child classes.

+   3. If a class is derived privately from a base class, then
+   
+     a. no members of the base class are inherited.
+   
+     b. all members are accessible by the derived class.
+   
+     c. all the members are inherited by the class, but are hidden and cannot be accessed.
+   
+     d. no derivation of the class gives an error.

4. What will be the output of the following C++ code?

```
```cpp
#include <iostream>
#include <string>
using namespace std;
class A
{
    float d;
public:
    virtual void func(){
        cout<<"Hello this is class A\\n";
    }
};
class B: public A
{
    int a = 15;
public:
    void func(){
        cout<<"Hello this is class B\\n";
    }
};
int main(int argc, char const *argv[])
{
    A *a = new A();
    B b;
    a = &b;
    a->func();
    return 0;
}
```
```

+   a. Hello this is class A
+   
+   b. Hello this is class B