```
{
    cout<<add(5,6)<<endl;
    cout<<oct<<add(5,6);
}
```

```
int add(int a,int b)
{
    return a+b;
}
```

Output
11
13

# # iomanip.h

This is a header file used for input/output manipulation. We shall include it for various purposes required. It has various functions,macros and classes included in it. Some of them are very useful and we shall discuss them.

+   1. setprecision()
+   2. setbase()
+   3. setw()

# ## setbase()

setbase() is an alternative to those three different macros oct, dec and hex.

```
#include<iostream>
#include<iomanip>
using namespace std;
int main()
{
    cout<<setbase(8)<<17<<endl;
    cout<<setbase(10)<<17<<endl;
}
```