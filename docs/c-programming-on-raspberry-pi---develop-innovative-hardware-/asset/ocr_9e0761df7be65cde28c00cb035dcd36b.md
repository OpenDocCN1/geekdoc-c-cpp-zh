Author: Dogan Ibrahim
File : TriangleArea.c
Date : December 2020

```
#include <stdio.h>

int main(void)
{
    float Base, Height, Area;
    printf("\nArea of a Triangle\n\n");
    printf("Enter base: ");
    scanf("%f", &Base);
    printf("Enter Height: ");
    scanf("%f", &Height);
    Area = Base * Height / 2.0;
    printf("Area = %f\n", Area);
    return 0;
}
```

Figure 3.1 Program: TriangleArea.c

At the beginning of the program, variables Base, Height and Area are declared as floating-point variables. The program then displays the heading Area of a Triangle. New lines are printed before and after displaying this heading. The text Enter base: is displayed and the user is requested to enter the base of the triangle which is stored in variable Base. Notice that scanf requires the memory address of the variable to store the data. Then height is requested from the user. The area of the triangle is calculated and displayed on screen. Figure 3.2 shows an example run of the program.

```
pi@raspberrypi:~ $ gcc -o Area TriangleArea.c
pi@raspberrypi:~ $ ./Area

Area of a Triangle

Enter base: 12.0
Enter Height: 10.4
Area = 62.399998
pi@raspberrypi:~ $
```

Figure 3.2 Example run of the program

We can change the number of decimal places using the %f statement. The general format of this statement is:

%n.df    where n is the total length of the number to be displayed and d is the number