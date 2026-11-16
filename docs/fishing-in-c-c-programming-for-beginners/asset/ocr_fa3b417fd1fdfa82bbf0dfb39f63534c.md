```
{
    int a;
    char b[4];
};
union un modify_union();
int main()
{
    union un un1;
    un1=modify_union();
    cout<<un1.a;
    return 0;
}
union un modify_union()
{
    union un unx;
    unx.a=3;
    return unx;
}
```

Output
3

# typedef

It is used to give aliases to a data type e.g.

Consider the following program:

```
#include<iostream>
using namespace std;
typedef unsigned long int uli;
```