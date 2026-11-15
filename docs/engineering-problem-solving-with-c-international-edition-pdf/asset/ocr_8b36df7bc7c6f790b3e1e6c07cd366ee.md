```
void eliminate(double a[] [N+1], int n, int index)
{
    // Declare objects.
    double scale_factor;

    // Eliminate object from equations.
    // for row i=index+1; rowN; ++row)
    {
        scale_factor = -a[row] [index]/a[index] [index];
        a[row] [index] = 0;
        for (int col=index+1; col<=n; ++col)
        {
            a[row] [col] += a[index] [col]*scale_factor;
        }
    }

    // Void return.
    return;
}
```

```
/*--------------------------------------------------*/
/* This function performs the back substitution. */
/*--------------------------------------------------*/
void back_substitute(double a[] [N+1], int n,
                     double soln[])
{
    // Perform back substitution in each equation.
    soln[n-1] = a[n-1] [n]/a[n-1] [n-1];
    for (int row=n-2; row>=0; --row)
    {
        for (int col=n-1; col>=row+1; --col)
        {
            a[row] [n] -= soln[col]*a[row] [col];
        }
        soln[row] = a[row] [n]/a[row] [row];
    }

    // Void return.
    return;
}
/*--------------------------------------------------*/
```

To handle larger systems of equations, the symbolic constant _N_ must be changed; the steps in the Gauss elimination do not need any modifications. The program interaction using the data from the hand example is as follows:

Enter resistor values in ohms:
(R1, R2, R3, R4, R5)
1 1 1 1 1
Enter voltage values in volts:
(V1, V2)
5 5