```
```cpp
x[3]=67;

// From this statement onwards dynamic array will be created.
int i=0;
cout<<"Dynamic array elements are"<<endl;
while(i<3)
{
cout<<"x[i] i="<<i<<"  "<<x[i]<<endl;
i++;
}
cout<<"y ="<<*y<<endl;
getch();
return 0;
}
```
```

```
```cpp
// Program to initialize the dynamic pointer.
#include<conio.h>
int main()
{
int *y;
clrscr();
y=new int(45);
int i=0;
cout<<"y ="<<*y<<endl; //Output will be 45
getch();
return 0;
}
```
```

# 2.4.6    Array of pointers

Array of pointers is an array that holds the pointers (addresses). Usage of array pointer is significant in cases where we need to store the addresses of various pointers of similar type. Array of pointer facilitate the ease of accessibility at the same time improves the efficiency of the program written. Primarily array of pointer is used to deal with double dimensional array type of problems. For instance, if we intend to store two or more arrays, then we can use pointer arrays. Example to access three array using array of pointers has been depicted in the following program.