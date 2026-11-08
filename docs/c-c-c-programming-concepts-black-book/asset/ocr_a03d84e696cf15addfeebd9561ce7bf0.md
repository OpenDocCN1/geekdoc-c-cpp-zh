The output of the preceding program is:

![](bbox=[0.244, 0.182, 0.797, 0.26])

+   13. Write a C++ Program to extend an existing enums.

```
~~~cpp
#include<iostream>
using namespace std;
int main()
{
    enum enumerator_1
    {
        var1,
        var2,
        var3,
        final_value = var3
    };
    //Print out the actual enumerator values
    cout<<"\nThe enumerator_1 values are: ";
    for(int i = 0; i <= final_value; i++)
        cout<<enumerator_1(i)<<" ";
    cout<<endl;
    enum extendedenumerator_1
    {
        var4 = final_value + 1,
        var5,
        var6,
        new_final_value = var6
    };
    //Print out the extended enumerator values
    cout<<"\nThe extended enumerator_1 values are : ";
    for(int i = 0; i <= new_final_value; i++)
    {
        cout<<extendedenumerator_1(i)<<" ";
    }
    cout<<endl;
    return 0;
}
~~~
```

The output of the preceding program is:

![](bbox=[0.244, 0.678, 0.792, 0.741])

+   14. Write a program to show Synchronous and Asynchronous calls in C++.

```
~~~cpp
#include <windows.h>
#include <process.h>
#include <iostream>
~~~
```