```
if(i!=7)
    cout<<"i is not 7";
else
    cout<<"i is 7";
}
```

Output

i is not 7

If you want to use more than one statement in if...else then you will have to use {...} otherwise the compiler will consider only one statement which is next to if...else under if and else. E.g. consider the following code

```
#include<iostream>
using namespace std;
int main()
{
    int num=53;
    if(num%5==0)
        cout<<"The number is divisible by 5";
        cout<<"The number is also divisible by 1";
    else
        cout<<"The number is not divisible by 5";
}
```

This program will give a compile error, “else without a previous if”. So, the correct one will be

```
#include<iostream>
using namespace std;
int main()
{
    int num=53;
    if(num%5==0)
```