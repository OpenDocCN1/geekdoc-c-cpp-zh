```
getch();
}
```

# OUTPUT :

s1 = 26

s2 = 100

s3 = 676

# EXPLANATION :

Before expanding the function as function call is encountered compiler first computes the expression written as argument and make a single argument. So square (2+3) first turned into square (5) then expanded, similarly square (3*4-5+6/2) turned into square (10) and finally square (+ +s1) turned into square (26).

# /*PROG 5.21 SQR OF A NUMBER USING MACRO*/

```
#include <iostream.h>
#define SQR(x) (x*x)
#include <conio.h>

void main()
{
    int s1 = SQR(2 + 3);
    int s2 = SQR(3*4 - 5 + 6/2);
    int s3 = SQR(+ +s1);

    clrscr();
    cout << "s1 = " << s1 << endl;
    cout << "s2 = " << s2 << endl;
    cout << "s3 = " << s3 << endl;
    getch();
}
```

# OUTPUT :

s1 = 13

s2 = 41

s3 = 156

# EXPLANATION :

The side effect of macro can be seen in the above program. When macro SQR is expanded all three statements appear as :
    int s1 = 2 + 3*2 + 3;