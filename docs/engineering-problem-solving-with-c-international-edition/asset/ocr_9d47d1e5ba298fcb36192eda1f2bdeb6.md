```
```
/*
* This function evaluates the sinc function.
*/
double sinc(double x)
{
    if (fabs(x) < 0.0001)
        return 1.0;
    else
        return sin(PI*x)/(PI*x);
}
/*-----------------------------------------------------------*/
```
```

The following output represents an example interaction that could occur with either program:

```
```
Enter endpoints a and b (a<b):
-2 2
x and sinc(x)
-2.000000 0.000000
-1.800000 -0.103943
-1.600000 -0.189207
-1.400000 -0.216236
-1.200000 -0.155915
-1.000000 0.000000
-0.800000 0.233872
-0.600000 0.504551
-0.400000 0.756827
-0.200000 0.935489
0.000000 1.000000
0.200000 0.935489
0.400000 0.756827
0.600000 0.504551
0.800000 0.233872
1.000000 0.000000
1.200000 -0.155915
1.400000 -0.216236
1.600000 -0.189207
1.800000 -0.103943
2.000000 0.000000
```
```

Figure 4.3 contains plots of the 21 values computed for four different intervals [a, b]. The program computes only 21 values, so the resolution in the plots is affected by the size of the interval—a smaller interval has better resolution than a larger interval. Note that the main function of Solution 2 is easier to read because it is shorter than the main function in the first solution. Now that you have an example of a program with a programmer-defined function, we present a more general discussion of the statements in a function.