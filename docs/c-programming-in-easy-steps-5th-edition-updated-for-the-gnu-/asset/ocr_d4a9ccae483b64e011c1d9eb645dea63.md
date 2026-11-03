# forloop.c

2 Add a main function that declares two integer variables to be used later as loop iteration counters

```
int main()
{
    int i, j;
}
```

3 Next, in the main function block, insert a for loop to output the loop counter value on each of three iterations

```
for(i = 1 ; i < 4 ; i++)
{
    printf( "Outer loop iteration %d\n", i );
}
```

4 At the end of the main function block, return a zero integer value, as required by the function declaration

```
return 0 ;
```

5 Save the program file, then compile and execute the program to see output from the for loop

![](bbox=[0.24, 0.64, 0.75, 0.8])

6 Now, in the loop block, insert a nested loop immediately after the existing output statement, to output the loop counter value on each of three inner loop iterations

```
for(j = 1 ; j < 4 ; j++)
{
    printf( "\tInner loop iteration %d\n", j );
}
```

7 Save the program file, then compile and execute the program once more to see output from both loops