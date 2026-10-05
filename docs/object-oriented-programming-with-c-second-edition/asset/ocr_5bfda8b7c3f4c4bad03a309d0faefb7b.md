```
int x,y;
x=10;
int &iRef=x;
y=iRef;              //same as y=x;
cout<<x<<endl;
y++;                   //x and iRef unchanged
cout<<x<<endl<<iRef<<endl<<y;
}
/*End of reference02.cpp*/
```

# Output

10
10
10
11

A reference variable can be a function argument and thus change the value of the parameter that is passed to it in the function call. Listing 1.18 is an illustrative example.

# Listing 1.18 Passing by reference

# Output

11

Functions can return by reference also. See Listing 1.19.

# Listing 1.19 Returning by reference

```
/*Beginning of reference04.cpp*/
#include<iostream.h>
int &larger(int &, int &);
int main()
{
    int x,y;
    x=10;
    y=20;
    int &r=larger(x,y);
    r=-1;
    cout<<x<<endl<<y<<endl;
}
```