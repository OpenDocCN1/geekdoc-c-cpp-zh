We can even pass information to the function telling the function to draw the line with a certain width and with a certain character:

```
// funct3.c
#include <stdio.h>
void printLine(int width, char ch);
int main(void) {
    int i;
    printLine(60, '*');
    printf("%15s%15s%15s\n", "Number", "Square", "Cube");
    printLine(50, '-');
    for (i = 1; i <= 10; i++) {
        printf("%15d%15d%15d\n", i, i*i, i*i*i);
    }
    printLine(55, '+');
    return 0;
}
void printLine(int width, char ch) {
    int i;
    for (i = 1; i <= width; i++) {
        printf("%c", ch);
    }
    printf("\n");
}
```

********************************************************************

| Number | Square | Cube |
| :--- | :--- | :--- |
| 1 | 1 | 1 |
| 2 | 4 | 8 |
| 3 | 9 | 27 |
| 4 | 16 | 64 |
| 5 | 25 | 125 |
| 6 | 36 | 216 |
| 7 | 49 | 343 |
| 8 | 64 | 512 |
| 9 | 81 | 729 |
| 10 | 100 | 1000 |

********************************************************************