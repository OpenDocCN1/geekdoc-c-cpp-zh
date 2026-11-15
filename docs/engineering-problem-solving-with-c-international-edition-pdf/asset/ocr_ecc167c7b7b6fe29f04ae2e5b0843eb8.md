```
// Exit program.
return 0;
}
/*------------------------------------------------------------*
* This function generates a random integer                    *
* between specified limits a and b (a<b).                     *
*------------------------------------------------------------*/
int rand_int(int a, int b)
{
    return rand()%(b-a+1) + a;
}
/*------------------------------------------------------------*/
```

A sample set of values generated from this program's as follows:

```
Enter a positive integer seed value:
13
Enter integer limits a and b (a<b):
-5 5
Random Numbers:
3 1 4 -4 0 0 0 -3 0
```

Remember that the values generated are system dependent; you should not expect to get this same set of random numbers from a different compiler.

# Modify!

Use the program developed in this section to generate several sets of random integers in each of the following ranges using different seed values.

+   1. 0 through 500
+   2. -10 through 200
+   3. -50 through 10
+   4. -5 through 5

# Floating-Point Sequences

In many engineering problems, we need to generate random floating-point values in a specified interval [a, b]. The computation to convert an integer between 0 and RAND_MAX to a floating-point value between a and b has three steps. The value from the rand() function is first divided by RAND_MAX to generate a floating-point value between 0 and 1. The value between 0 and 1 is then multiplied by (b - a), which is the width of the interval [a, b], to give a value between 0 and (b - a). The value between 0 and b - a is then added to a to adjust so that it will be between a and b. These three steps are combined in the expression on the return statement in the following function.