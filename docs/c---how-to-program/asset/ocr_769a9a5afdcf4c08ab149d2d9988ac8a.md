sometimes across different compilers on the same platform. The output shows the results from our Windows system using the Visual C++ compiler. The size of a long double was 12 bytes on our Linux system using the GNU gcc compiler. The size of a long was 8 bytes and the size of a long double was 16 bytes on our Mac system using Xcode's LLVM compiler.

```
```c
// Fig. 7.17: fig07_17.c
// Using operator sizeof to determine standard data type sizes.
#include <stdio.h>

int main(void)
{
    char c;
    short s;
    int i;
    long l;
    long long ll;
    float f;
    double d;
    long double ld;
    int array[20]; // create array of 20 int elements
    int *ptr = array; // create pointer to array

    printf("\n    sizeof c = %u\t sizeof(char) = %u"
    "\n    sizeof s = %u\t sizeof(short) = %u"
    "\n    sizeof i = %u\t sizeof(int) = %u"
    "\n    sizeof l = %u\t sizeof(long) = %u"
    "\n    sizeof ll = %u\t sizeof(long long) = %u"
    "\n    sizeof f = %u\t sizeof(float) = %u"
    "\n    sizeof d = %u\t sizeof(double) = %u"
    "\n    sizeof ld = %u\t sizeof(long double) = %u"
    "\n    sizeof array = %u"
    "\n    sizeof ptr = %u",
    sizeof c, sizeof(char), sizeof s, sizeof(short), sizeof i,
    sizeof(int), sizeof l, sizeof(long), sizeof ll,
    sizeof(long long), sizeof f, sizeof(float), sizeof d,
    sizeof(double), sizeof ld, sizeof(long double),
    sizeof array, sizeof ptr);
}
```
```

| sizeof c = 1 | sizeof(char) = 1 |
| sizeof s = 2 | sizeof(short) = 2 |
| sizeof i = 4 | sizeof(int) = 4 |
| sizeof l = 4 | sizeof(long) = 4 |
| sizeof ll = 8 | sizeof(long long) = 8 |
| sizeof f = 4 | sizeof(float) = 4 |
| sizeof d = 8 | sizeof(double) = 8 |
| sizeof ld = 8 | sizeof(long double) = 8 |
| sizeof array = 80 |  |
| sizeof ptr = 4 |  |

Fig. 7.17 | Using operator sizeof to determine standard data type sizes.