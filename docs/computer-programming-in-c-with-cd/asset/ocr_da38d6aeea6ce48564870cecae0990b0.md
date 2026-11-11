```
```cpp
{
    c=b+get_a();
}
void display()
{
    cout<<"After Addition"<<endl;
    cout<<"a = "<<get_a()<<endl;
    cout<<"b = "<<b<<endl;
    cout<<"c = "<<c<<endl;
}
};
void main()
{
    B obj;
    obj.set_ab();
    obj.addition();
    obj.display();
}
```
```

```
```text
Output:

Enter the values for a and b variables
100
50
After Addition
a = 100
b = 50
c = 150
```
```

Q4. Create a program that displays an example of single inheritance with protected derivation.

Ans.

```
```cpp
#include <iostream.h>

class MyBase{
protected:
    int i, j;               /* private to MyBase, but accessible by
                               MyDerived */
public:
    void setdata(int a, int b) {
        i = a;
        j = b;
    }
    void showdata() {
        cout << "i : " << i << "\n" << "j : " << j << endl;
    }
};
class MyDerived : protected MyBase{    /* Inherit MyBase as
                                          protected */
```
```