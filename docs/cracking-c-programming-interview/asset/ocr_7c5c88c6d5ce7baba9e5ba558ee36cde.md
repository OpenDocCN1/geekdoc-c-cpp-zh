+   (b) 8 9
(c) 8
(d) 1 1

# 34. Evaluate the variables b, c, d, e, f, g, i, j?

```
#include<stdio.h>
int main()
{
    int b = 5-4+2*5;
    int c = 5&4&6;
    int d = 5&4 | 6;
    int e = 57*4-9*(3, 2);
    int h=8;
    int f = (h++, h++);
    int g = h++ + h++ + h++;
    int i = 7*8+6*7<6 7:6;
    int j = 2-3+4-8-5%4;
    return 0;
}
```

# 35. What is the output of the following program?

```
#include<stdio.h>
#define type_char char*
int main()
{
    type_char a , b; // line 1
    char c[10] , d[10];
    strcpy(c , "hello");
    strcpy(d , "world");
    a = c;
    b = d; //line 6
    printf("%c %c", a[2],b[2]); //line 7
    return 0;
}
```

+   (a) I