```
++c1;
cout<<c1.return_value();
}
```

Output

0

1

Similarly, we can overload the decrement operators too.

# Using return types in operator overloading

However, we cannot store the value since it has not returned anything. So, if we want to store the value in an object then we can return the value so that we can store it in an object. Following program illustrates this fact:

```
#include<iostream>
using namespace std;
class counting
{

int count;

public:

counting(){ count=0;}
void set_value(int a){count=a;}
int return_value(){return count;}
counting operator++();

};

counting counting::operator++()
{

++count;

counting cx;

cx.set_value(count);
```