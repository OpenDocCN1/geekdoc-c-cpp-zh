# Appendix A A.49

```
initgraph(&gd, &gm, "..\\bgi"); /*Initializing the graphics system*/
circle(320, 225, 50); /*Calling the built in function circle()*/
getch();
closegraph(); /*Shutting the graphics system*/
}
```

Output

![](bbox=[0.32, 0.38, 0.68, 0.58])

# EXAMPLE A.57 Write a program to draw a rectangle.

```
/*Program for demonstrating the use of built-in graphics functions of C*/
#include<conio.h>
#include<graphics.h>
#include<stdio.h>

void main()
{
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "..\\bgi"); /*Initializing the graphics system*/
    rectangle(320, 225, 50,100); /*Calling the built-in function rectangle()*/
    getch();
    closegraph(); /*Shutting the graphics system*/
}
```

Output

![](bbox=[0.32, 0.96, 0.68, 1.0])