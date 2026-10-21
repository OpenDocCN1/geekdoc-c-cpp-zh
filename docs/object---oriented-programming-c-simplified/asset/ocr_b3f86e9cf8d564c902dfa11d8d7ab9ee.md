```
getch();
}
```

# OUTPUT :

Enter ptr[0][0] element :10

Enter ptr[0][1] element :11

Enter ptr[0][2] element :12

Enter ptr[1][0] element :13

Enter ptr[1][1] element :14

Enter ptr[1][2] element :15

Enter ptr[2][0] element :16

Enter ptr[2][1] element :17

Enter ptr[2][2] element :18

Matrix is

10      11      12
13      14      15
16      17      18

EXPLANATION : The construction of dynamic 2-D array was explained in the chapter 4. The same logic is used here but it is put into the class.

# /*PROG 7.20 DYNAMIC CONSTRUCTION OF STRING */

```
#include <iostream.h>
#include <conio.h>
#include <string.h>

class string
{
    char *sname;
    int len;
```