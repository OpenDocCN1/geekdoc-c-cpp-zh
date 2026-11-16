```
catch(...)
{
    cout<<"Error occurred";
}
return 0;
}
```

Output

Error occurred

Ellipsis is used as last argument for catch, if integral or char error is not caught. So, you can rewrite the above program as follows:

```
#include<iostream>
using namespace std;
int main()
{
    try
    {
        long double*array=new long double[100000000000000000];
    }
    catch(int a)
    {
        cout<<"Integral Error occurred";
    }
    catch(char a)
    {
        cout<<"Char Error occurred";
    }
}
```