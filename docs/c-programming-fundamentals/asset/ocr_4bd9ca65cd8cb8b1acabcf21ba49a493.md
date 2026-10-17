# Code: Using Access Specifiers (Public, Private, and Protected)

```
```cpp
#include <iostream>
using namespace std;
class Parent {

    public:
    int p1=60;
    void showP()
    {
        cout<<"\nParent age is public " <<p1<< endl;
        cout<<"\nParent age is private " <<p2<< endl;
        cout<<"\nParent age is protected " <<p3<< endl;
    }
    private:
    int p2=12;
    protected:
    int p3=16;
};

class Child : public Parent
{

    public:
    int c1=20;
    void showC() {
        cout<< "\nChild age is public " <<c1<< endl;
        cout<< "\nChild age is private " <<c2<< endl;
        cout<< "\nChild age is protected " <<c3<< endl;
    }
    private:
    int c2;
    protected:
    int c3;
};

int main() {
    Child c;
    c.p2=36;
    c.p3=56;
    c.showP();
    c.showC();
    return 0;
}
```
```