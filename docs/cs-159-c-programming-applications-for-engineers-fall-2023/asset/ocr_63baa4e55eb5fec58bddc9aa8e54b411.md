```
void calcAvgs(int data[][COLS], float avgs[])
{
    int currentRow;
    int currentCol;
    int sum;

    for(currentRow = 0; currentRow < ROWS; currentRow++)
    {
        sum = 0;

        for(currentCol = 0; currentCol < COLS; currentCol++)
        {
            sum += data[currentRow][currentCol];
        }

        avgs[currentRow] = (float)sum / COLS;
    }
}
```

```
void printTable(int data[][COLS], float avgs[])
{
    int currentRow;
    int currentCol;

    for(currentRow = 0; currentRow < ROWS; currentRow++)
    {
        printf("Row #%d: ", currentRow + 1);

        for(currentCol = 0; currentCol < COLS; currentCol++)
        {
            printf("%d ", data[currentRow][currentCol]);
        }

        printf("Average: %.2f\n", avgs[currentRow]);
    }
}
```

# Why is it required to specify the extent of the second dimension in the function definition as seen above?

+   - The name of an array only stores where it begins in the memory of the computer. No information regarding dimensions is stored.