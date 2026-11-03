
```
printf("%2d", row);
for(j = 1; j <= COLUMNS ;j++)
{
    column = j;
    product[i][j] = row * column;
    printf("%4d", product[i][j]);
}
printf("\n");
}
```

### Output: MULTIPLICATION TABLE

|   | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 1 | 1 | 2 | 3 | 4 | 5 |
| 2 | 2 | 4 | 6 | 8 | 10 |
| 3 | 3 | 6 | 9 | 12 | 15 |
| 4 | 4 | 8 | 12 | 16 | 20 |
| 5 | 5 | 10 | 15 | 20 | 25 |

Fig. 8.5 Program to print multiplication table, using two-dimensional array

```
static int table[2][3] = {
    {1,1},
    {2}
};
```

will initialize the first two elements of the first row to one, the first element of the second row to two, and all other elements to zero.

When all the elements are to be initialized to zero, the following short-cut method may be used.

```
static int m[3][5] = { {0}, {0}, {0} };
```

The first element of each row is explicitly initialized to zero while other elements are automatically initialized to zero.

### Example 8.5

A survey to know the popularity of four cars (Ambassador, Fiat, Dolphin and Maruti) was conducted in four cities (Bombay, Calcutta, Delhi and Madras). Each person surveyed was asked to give his city and the type of car he was using. The results, in coded form, are tabulated as follows:

```
M 1 C 2 B 1 D 3 M 2 B 4
C 1 D 3 M 4 B 2 D 1 C 3
D 4 D 4 M 1 M 1 B 3 B 3
C 1 C 1 C 2 M 4 M 2 C 2
D 1 C 2 B 3 M 1 B 1 C 2
D 3 M 4 C 1 D 2 M 3 B 4
```

Codes represent the following information:

| City Code | City | Car Code | Car |
|---|---|---|---|
| M | Madras | 1 | Ambassador |
| D | Delhi | 2 | Fiat |
| C | Calcutta | 3 | Dolphin |
| B | Bombay | 4 | Maruti |

Write a program to produce a table showing popularity of various cars in four cities.

A two-dimensional array frequency is used as an accumulator to store the number of cars used, under various categories in each city. For example, the element frequency[i][j] denotes the number of cars of type j used in city i. The frequency is declared as an array of size 5 × 5 and all the elements are initialized to zero.

The program shown in Fig. 8.6 reads the city code and the car code, one set after another, from the terminal. Tabulation ends when the letter X is read in place of a city code.

## 8.5 MULTIDIMENSIONAL ARRAYS

C allows arrays of three or more dimensions. The exact limit is determined by the compiler. The general form of a multidimensional array is

```
type array_name[s1][s2][s3]....[sm];
```

where si is the size of the ith dimension. Some examples are:

```
int survey[3][5][12];
float table[5][4][5][3];
```

survey is a three-dimensional array declared to contain 180 integer type elements. Similarly table is a four-dimensional array containing 300 elements of floating-point type.

The array survey may represent a survey data of rainfall during the last three years from January to December in five cities.

### Program

8.16 C Programming and Data Structures

```
/***************************************************************/
/* PROGRAM TO TABULATE SURVEY DATA */
/***************************************************************/
main()
{
    int i, j, car;
    static int frequency[5][5] = { {0}, {0}, {0}, {0}, {0} };
    char city;
    printf("For each person, enter the city code\n");
    printf("followed by the car code.\n");
    printf("Enter the letter X to indicate end.\n");
    /* ...........................................TABULATION BEGINS................................ */
    for(i=1; i<100 ;i++)
    {
        scanf("%c",&city);
        if(city == 'X')
            break;
        scanf("%d",&car);
        switch(city)
        {
        case 'B' : frequency[1][car]++;
            break;
        case 'C' : frequency[2][car]++;
            break;
        case 'D' : frequency[3][car]++;
            break;
        case 'M' : frequency[4][car]++;
            break;
        }
    }
    /* .................... TABULATION COMPLETED AND PRINTING BEGINS ... */
    printf("\n\n");
    printf(" POPULARITY TABLE\n\n");
    printf(" City Ambassador Fiat Dolphin Maruti\n");
    printf("---------------------------------------\n");
    for(i = 1 ; i <= 4; i++)
    {
        switch(i)
        {
        case 1: printf("Bombay ");
            break;
        case 2: printf("Calcutta ");
            break;
        case 3: printf("Delhi ");
            break;
        case 4: printf("Madras ");
            break;
        }
        for(j = 1 ; j <= 4; j++ )
            printf("%7d", frequency[i][j]);
        printf("\n");
    }
    /* .................... PRINTING ENDS ........................ */
}
```

### Output

For each person, enter the city code followed by the car code.

Enter the letter X to indicate end.

| City | Ambassador | Fiat | Dolphin | Maruti |
|---|---|---|---|---|
| Bombay | 2 | 1 | 3 | 2 |
| Calcutta | 4 | 1 | 1 | 0 |
| Delhi | 2 | 1 | 3 | 2 |
| Madras | 4 | 1 | 1 | 4 |

Fig. 8.6 Program to tabulate a survey data

If the first index denotes year, the second city and the third month, then the element survey[1][2][9] denotes the rainfall in the month of October during the second year in city-3. Remember that a three-dimensional array can be represented as a series of two-dimensional arrays as shown below:

![](img/65953ea584e494f3d396b2252cb5ea53_213_0.png)

![](img/65953ea584e494f3d396b2252cb5ea53_213_1.png)

## CASE STUDIES

### 1. Median of a List of Numbers

When all the items in a list are arranged in order, the middle value which divides the items into two parts with equal number of items on either side is called the median. Odd number of items have just one middle value while even number of items have two middle values. The median for even number of items is therefore designated as the average of the two middle values.

The major steps for finding the median are as follows:

- 1. Read the items into an array while keeping a count of the items.
- 2. Sort the items in increasing order.
- 3. Compute median.

The program and sample output are shown in Fig. 8.7. The sorting algorithm used is as follows:

- 1. Compare the first two elements in the list, say a[1], and a[2]. If a[2] is smaller than a[1], then interchange their values.
- 2. Compare a[2] and a[3]; interchange them if a[3] is smaller than a[2].
- 3. Continue this process till the last two elements are compared and interchanged.
- 4. Repeat the above steps n-1 times.

In repeated trips through the array, the smallest elements ‘bubble up’ to the top. Because of this bubbling up effect, this algorithm is called bubble sorting. The bubbling effect is illustrated below for four items.

8.18 C Programming and Data Structures

![](img/65953ea584e494f3d396b2252cb5ea53_214_0.png)

During the first trip, three pairs of items are compared and interchanged whenever needed. It should be noted that the number 80, the largest among the items, has been moved to the bottom at the end of the first trip. This means that the element 80 (the last item in the new list) need not be considered any further. Therefore, trip-2 requires only two pairs to be compared. This time, the number 65 (the second largest value) has been moved down the list. Notice that each trip brings the smallest value 10 up by one level.

The number of steps required in a trip is reduced by one for each trip made. The entire process will be over when a trip contains only one step. If the list contains n elements, then the number of comparisons involved would be n(n-1)/2.

### Program

```
/* ****************************************************************** */
/* PROGRAM TO SORT A LIST AND FIND ITS MEDIAN */
/* ****************************************************************** */
#define N 10
main()
{
    int i,j,n;
    float median, a[N], t;
    printf("Enter the number of items\n");
    scanf("%d", &n);
    /* Reading items into array */
    printf("Input %d values\n",n);
    for (i = 1; i <= n; i++)
        scanf("%f", &a[i]);
    /* Sorting begins */
    for (i = 1; i <= n-1; i++)
    { /* Trip i begins */
        for (j = 1; j <= n- i; j++)
        {
            if (a[j] <= a[j+1])
            { /* Interchanging values */
                t = a[j];
                a[j] = a[j+1];
                a[j+1] = t;
            }
            else
                continue;
        }
    } /* sorting ends */
    /* calculation of median */
    if (n % 2 == 0)
        median = (a[n/2] + a[n/2 + 1])/2.0;
    else
        median = a[n/2 + 1];
    /* Printing */
    for (i = 1; i <= n; i++)
        printf("%f", a[i]);
    printf("\nMedian is %f\n", median);
}
```

### Output

```
Enter the number of items
5
Input 5 values
1.111 2.222 3.333 4.444 5.555
5.555000 4.444000 3.333000 2.222000 1.111000
Median is 3.333000
Enter the number of items
6
Input 6 values
3 5 8 9 4 6
9.000000 8.000000 6.000000 5.000000 4.000000 3.000000
Median is 5.500000
```
