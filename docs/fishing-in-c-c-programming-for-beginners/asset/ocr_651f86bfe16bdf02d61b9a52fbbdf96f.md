```
cout<<c1;
return 0;
}
```

```
enum color modify_enum()
{
    return green;
}
```

Output

2

# Union

Union is a derived data type, which resembles structure in look but is not. Consider the following union

```
union un
{
int a;
char b[4];
};
```

Here, since I am using a 64 bit compiler, so I used char b[4]. If you are using a 32 bit compiler, then you should write char b[2]. So, the amazing thing about union is that it divides the memory among its element, i.e its size is 4 bytes only, not 8 bytes.

Consider the following program in 64 bit compiler:

```
#include<iostream>
using namespace std;
union un
{
    int a;
    char b[4];
```