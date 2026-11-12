# The Bubble Sort

Note: The code below is a variation of the Bubble Sort and is different from the code given in the book.

```
#define NUMDATA 10

void bubbleSort(int[]);
void getData(int[]);
void printData(int[]);

int main(void)
{
    int data[NUMDATA]; //ARRAY TO HOLD DATA TO SORT
    getData(data);
    printData(data); //PRINT BEFORE STATE
    bubbleSort(data);
    printData(data); //PRINT AFTER STATE
    return(0);
}

void printData(int x[])
{
    int lcv; //LOOP CONTROL VARIABLE TO ACCESS ARRAY
    for(lcv = 0; lcv < NUMDATA; lcv++)
    {
        printf("x[%d] = %d\n", lcv, x[lcv]);
    }
}

void getData(int x[])
{
    int lcv; //LOOP CONTROL VARIABLE TO GET DATA
    for(lcv = 0; lcv < NUMDATA; lcv++)
    {
        scanf("%d", &x[lcv]);
    }
}
```