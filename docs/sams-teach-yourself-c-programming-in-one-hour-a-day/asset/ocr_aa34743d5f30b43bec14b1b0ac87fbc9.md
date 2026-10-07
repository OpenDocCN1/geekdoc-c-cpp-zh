# Input ▼

LISTING 9.4 scanf.c: Passing an Array to a Function

```
1 /* arraypass.c--Passing an array to a function. */
2:
3 #include <stdio.h>
4:
5 #define MAX 10
6:
7 int array[MAX], count;
8:
9 int largest(int num_array[], int length);
10:
11 int main(void )
12 {
13:
14     /* Input MAX values from the keyboard. */
15:
16     for (count = 0; count < MAX; count++)
17     {
18         printf("Enter an integer value: ");
19         scanf("%d", &array[count]);
20     }
21:
22     /* Call the function and display the return value. */
23     printf("\n\nLargest value = %d\n", largest(array, MAX));
24:
25     return 0;
26 }
27 /* Function largest() returns the largest value */
28 /* in an integer array */
29 int largest(int num_array[], int length)
30 {
31     int count, biggest;
32:
33     for (count = 0; count < length; count++)
34     {
35         if (count == 0)
36             0
37             biggest = num_array[count];
38         if (num_array[count] > biggest)
39             biggest = num_array[count];
40     }
41:
42     return biggest;
43 }
```