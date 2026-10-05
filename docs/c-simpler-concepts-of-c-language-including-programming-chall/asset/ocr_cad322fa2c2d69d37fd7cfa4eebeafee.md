# 54 C-SIMPLER

```
#include<stdio.h>
void main() {
    int a,b;
    int choice;
    printf("choose the LOGICAL operation to be performed!\n" "1.AND (&&) \n2.OR (||)\n3.NOT (!)\n4.Exit\n");
    scaf("%d",&choice);
    printf("\nenter the first number..\n"); scanf("%d",&a);
    printf("\nEnter the second number..\n"); scanf("%d",&b);
    do{
        switch (choice) {
            case 1:
                printf("%d && %d = %d\n",a,b,a&&b);
                break;
            case 2:
                printf("%d || %d = %d\n",a,b,a||b);
                break;
            case 3:
                printf("!a=%d, !b=%d\n",a,b);
                break;
        }
        printf("\nchoose the LOGICAL operation to be performed!\n" "1.AND (&&) \n2.OR (||)\n3.NOT (!)\n4.Exit\n");
        scaf("%d",&choice);
    } while (choice!=4);
    getch();
```

# Program 4.1 Logical Operators

![](bbox=[0.134, 0.621, 0.866, 0.923])

Output 4.1