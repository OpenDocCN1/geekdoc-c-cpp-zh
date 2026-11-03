# A simple example of a do...while

```
do {
  printf("Input a number \n");
  number = getnum();
} while (number > 0);
```

This segment of a program reads a number from the keyboard until a zero or a negative number is keyed in, and assigned to the sentinel variable number.

The test conditions may have compound relations as well. For instance, the statement while (number > 0 && number < 100); in the above example would cause the loop to be executed as long as the number keyed in lies between 0 and 100.

Consider another example:

```
I = 1;
  sum = 0;
  do {
    sum = sum + I;
    I = I+2;
  } while(sum < 40 || I < 10);
  printf("%d %d\n", I, sum);
```

The loop will be executed as long as one of the two relations is true.

# EXAMPLE 4.11 A program to print the multiplication table from 1 x 1 to 12 x 12 is given in Fig. 4.13.

This program contains two do...while loops nested form. The outer loop is controlled by the variable row and executed 12 times. The inner loop is controlled by the variable column and is executed 10 times, each time the outer loop is executed. That is, the inner loop is executed a total of 120 times, each time printing a value in the table.

```
#define COLMAX 10
#define ROWMAX 12
main()
{
  int row,column, y;
  row = 1;
  printf(" MULTIPLICATION TABLE \n");
  printf("\n");
  do
  {
    column = 1;
    /*........OUTER LOOP BEGINS........*/
    do
    {
      y = row * column;
      printf("%d ", y);
      column = column + 1;
    } while(column <= COLMAX);
    printf("\n");
    row = row + 1;
  } while(row <= ROWMAX);
}
```