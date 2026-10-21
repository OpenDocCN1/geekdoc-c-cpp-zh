```
swap(x,y);

cout << "After calling swap\n";
cout << "x=" << x << "\t" << "y=" << y << endl;
}

void swap(int & rx,int & ry)
{
    rx = rx + ry;
    ry = rx - ry;
    rx = rx - ry;
}
```

# OUTPUT :

Enter the two numbers

23  45

Before calling swap

x=23   y=45

After calling swap

x=45   y=23

# EXPLANATION : The program remains same but the logic to swap two values changes. Without using third variable we change the values. Check the logic against any value of x and y. Take an example for x=10 and y=5

x = x + y => x = 10 + 5 => x =15
 y = x - y => y = 15 - 5 => y = 10
 x = x - y => y = 15 - 10 => x= 5

```
/*PROG 5.10 REFERENCE VARIABLE AS FUNCTION ARGUMENT SWAPPING TWO VALUES VER 3*/

#include <iostream.h>
#include <conio.h>

void main()
{
```