```
getch();
}
float square(float x)
{
    float y;
    y=x*x;
    return(y);
}
```

# 115. Wap to swap two values using functions call by value.

```
#include<stdio.h>
#include<conio.h>
void myswap(int x,int y);/* function prototype*/
void main()
{
    int a=10,b=20;
    myswap(a,b);
    printf("\n a=%d,b=%d",a,b);
    getch();
}
void myswap(int x, int y)
{
    int t;
    t=x;
    x=y;
    y=t;
    printf(\n x=%d,y=%d",x,y);
}
```

# 116. Wap to swap two values using functions call by reference.

```
#include<stdio.h>
#include<conio.h>
```