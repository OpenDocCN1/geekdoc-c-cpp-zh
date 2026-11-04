```
```c
/*---------------------------------------------------------
       SERIALLY CONNECTED RESISTORS
       ==========================================
Total resistance of serially connected resistors

Author: Dogan Ibrahim
File  : SerialResistors.c
Date  : December 2020
---------------------------------------------------------*/
#include <stdio.h>

int main(void)
{
    int no, k, R, Total;

    printf("\nSerially Connected Resistors");
    printf("\n====================================\n");

    printf("How many resistors are there? ");
    scanf("%d", &no);

    k = 1;
    Total = 0;

    while(k <= no)
    {
        printf("Enter resistance (Ohms) of Resistor %d: ", k);
        scanf("%d", &R);
        Total = Total + R;
        k++;
    }

    printf("\nTotal resistance = %d Ohms\n", Total);
    return 0;
}
```
```

Figure 3.9 Program: SerialResistors.c