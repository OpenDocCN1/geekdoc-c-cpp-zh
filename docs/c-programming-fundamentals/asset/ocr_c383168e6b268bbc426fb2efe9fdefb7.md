+   c. Error
+   d. Segmentation Fault

# 5. Write the output of the following code.

```
#include <iostream>
#include <string>
using namespace std;
class A
{
    float d;
    public:
    virtual void func(){
        cout<<"Hello this is class A\n";
    }
};
class B: public A
{
    int a = 15;
    public:
    void func(){
        cout<<"Hello this is class B\n";
    }
};
int main(int argc, char const *argv[])
{
    A *a;
    a->func();
    return 0;
}
```

+   a. Hello this is class A
+   b. Hello this is class B
+   c. Error
+   d. Segmentation Fault

# 6. What will be the output of the following C++ code?

```
#include <iostream>
#include <string>
using namespace std;
class A{
    float d;
```