sometimes across different compilers on the same platform. The output shows the results from our Windows system using the Visual C++ compiler. The size of a long double was 12 bytes on our Linux system using the GNU gcc compiler. The size of a long was 8 bytes and the size of a long double was 16 bytes on our Mac system using Xcode's LLVM compiler.

```
```c
1 // Fig. 7.17: fig07_17.c
2 // Using operator sizeof to determine standard data type sizes.
3 #include <stdio.h>
4
5 int main(void)
6 {
7    char c;
8    short s;
9    int i;
10   long l;
11   long long ll;
12   float f;
13   double d;
14   long double ld;
15   int array[20]; // create array of 20 int elements
16   int *ptr = array; // create pointer to array
17
18   printf( "sizeof c = %u\tsizeof(char) = %u"
19          "\n     sizeof s = %u\tsizeof(short) = %u"
20          "\n     sizeof i = %u\tsizeof(int) = %u"
21          "\n     sizeof l = %u\tsizeof(long) = %u"
22          "\n     sizeof ll = %u\tsizeof(long long) = %u"
23          "\n     sizeof f = %u\tsizeof(float) = %u"
24          "\n     sizeof d = %u\tsizeof(double) = %u"
25          "\n     sizeof ld = %u\tsizeof(long double) = %u"
26          "\n     sizeof array = %u"
27          "\n     sizeof ptr = %u\n",
28          sizeof c, sizeof(char), sizeof s, sizeof(short), sizeof i,
29          sizeof(int), sizeof l, sizeof(long), sizeof ll,
30          sizeof(long long), sizeof f, sizeof(float), sizeof d,
31          sizeof(double), sizeof ld, sizeof(long double),
32          sizeof array, sizeof ptr);
33 }
```
```

```
```
sizeof c = 1            sizeof(char) = 1
sizeof s = 2            sizeof(short) = 2
sizeof i = 4            sizeof(int) = 4
sizeof l = 4            sizeof(long) = 4
sizeof ll = 8           sizeof(long long) = 8
sizeof f = 4            sizeof(float) = 4
sizeof d = 8            sizeof(double) = 8
sizeof ld = 8           sizeof(long double) = 8
sizeof array = 80
sizeof ptr = 4
```
```

Fig. 7.17 | Using operator sizeof to determine standard data type sizes.