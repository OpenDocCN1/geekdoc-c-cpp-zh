# A four-dimensional array:

# A three-dimensional array:

Problem, calculate the average of each row in a two-dimensional array:

```
#define ROWS 5
#define COLS 4
void printTable(int [][COLS], float []);
void calcAvgs(int [][COLS], float []);
int main(void)
{
    float avgs[ROWS];
    int table[ROWS][COLS] =
    {
        {1, 2, 3, 4},
        {2, 3, 4, 5},
        {3, 4, 5, 6},
        {4, 5, 6, 7},
        {5, 6, 7, 8}
    };
    calcAvgs(table, avgs);
    printTable(table, avgs);
    return(0);
}
```