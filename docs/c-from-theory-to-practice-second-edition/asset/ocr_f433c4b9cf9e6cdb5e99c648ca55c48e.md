```
/* We choose three random places. The numbers stored in
these places will be drawn in the next lottery. */
pos1 = rand()%SIZE;
do
{
    pos2 = rand()%SIZE;
} while(pos1 == pos2);
do
{
    pos3 = rand()%SIZE;
} while((pos1 == pos3) || (pos2 == pos3));
/* Next lottery. */
for(i = 0; i < SIZE; i++)
{
    if((i == pos1) || (i == pos2) || (i == pos3))
    {
        printf("%d ", arr[i]);
        continue;
    }
    arr[i] = rand()%101;
    printf("%d ", arr[i]);
}
return 0;
}
```

Comments: The primary goal of this program is to show you that betting software can be written in a way to manipulate the winning results. Therefore, stay away from betting sites that advertise big profits in online lotteries. The big profits they promise are not for you, but for their owners.

# Two-Dimensional Arrays

The form of a two-dimensional array resembles that of a matrix in math; it is an array of elements of the same type arranged in rows and columns. As with one-dimensional arrays, we'll use arithmetic types in our examples. In the following chapters, you'll see more application examples. Besides numbers, a two-dimensional array is often used to store strings; you'll see this application in Chapter 10.

# Declaring Arrays

To declare a two-dimensional array, we must specify its name, its data type, and the number of its rows and columns, like this:

```
data_type array_name[number_of_rows][number_of_columns]
```