D — Delhi    2 — Fiat
C — Calcutta    3 — Dolphin
B — Bombay    4 — Maruti

Write a program to produce a table showing popularity of various cars in four cities.

A two-dimensional array frequency is used as an accumulator to store the number of cars used, under various categories in each city. For example, the element frequency [i][j] denotes the number of cars of type j used in city i. The frequency is declared as an array of size 5 × 5 and all the elements are initialized to zero.

The program shown in Fig. 8.6 reads the city code and the car code, one set after another, from the terminal. Tabulation ends when the letter X is read in place of a city code.

# 8.5 MULTIDIMENSIONAL ARRAYS

C allows arrays of three or more dimensions. The exact limit is determined by the compiler. The general form of a multidimensional array is

```
type array_name[s1][s2][s3]....[sm];
```

where si is the size of the ith dimension. Some example are:

```
int survey[3][5][12];
float table[5][4][5][3];
```

survey is a three-dimensional array declared to contain 180 integer type elements. Similarly table is a four-dimensional array containing 300 elements of floating-point type.

The array survey may represent a survey data of rainfall during the last three years from January to December in five cities.

```
Program
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
```