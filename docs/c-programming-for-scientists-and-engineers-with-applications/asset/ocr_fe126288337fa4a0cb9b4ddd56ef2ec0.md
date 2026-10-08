```
{
  scanf("%d", &a[i]);
}
```

The data entered from the terminal keyboard and stored in the memory allocated for the array is as follows:

45 56 76 93 15

Notice that when the numbers are entered from the keyboard, 45 is stored in a[0], 56 is stored in a[1], and so on.

| a[0] | 45 |
| a[1] | 56 |
| a[2] | 76 |
| a[3] | 93 |
| a[4] | 15 |

Input from a Data File "myfilein.data"

```
#define SIZE 5
FILE *inptr;
int i, a[SIZE];
inptr = fopen("myfilein.dat", "r");
for(i = 0; i < SIZE; i++)
{
  fscanf(inptr, "%d", &a[i]);
}
```

The data is read from a data file "myfilein.dat" stored in the memory allocated for the array as shown.

![](bbox=[0.283, 0.737, 0.568, 0.788])

Notice that the integer value 45 read from the data file "myfilein.dat" is stored in a[0], 56 is stored in a[1], and so on. Similarly the input into a one-dimensional array of data type float or double may be input from a standard input device or from a data file.