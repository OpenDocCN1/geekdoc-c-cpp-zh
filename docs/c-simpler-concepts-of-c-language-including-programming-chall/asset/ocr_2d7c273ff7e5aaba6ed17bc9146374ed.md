# 24 C-SIMPLER

Similarly, one can leave the increment/decrement part, by including an increment/
decrement statement just before the loop terminates.

Program 2.6 and Output 2.6 explains printing a pattern using *

```
//for_loop.c
#include<stdio.h>
#include<conio.h>
main() {
    int i,j;
    for (i=0;i<7;i++) {
        for (j=0;j<=1;j++) {
            printf("*");
        }
    }
    getch();
}
```

# Program 2.6 * pattern printing with loop.

![](bbox=[0.11, 0.455, 0.89, 0.635])

Output 2.6 * pattern printing with for Program 2.6.

Program 2.7 given below explains printing even and odd numbers from 0 to 19,
Output 2.7 Shows the Sample output.

```
#include<stdio.h>
#include<conio.h>
void main() {
    int i,j;
    for(i=0;i<20;i++) {
        if(i%2==0)
            printf("even:%d\t\t",i);
        else
            printf("odd:%d\t\t",i);
    }
    getch();
}
```

# Program 2.7 Sample program for 'for' loop.