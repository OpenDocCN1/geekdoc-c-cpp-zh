# Output:

```
    Enter an integer : 5
    5 * 1 = 5
    5 * 2 = 10
    5 * 3 = 15
    5 * 4 = 20
```

![](bbox=[0.395, 0.254, 0.583, 0.543])

# 16) Write a program for calculating the result of sine series.

sin(x)=(x^1/1!) - (x^3/3!) + (x^7/7!) - ......

# Algorithm:

```
    Step 1: Start
    Step 2: Initialize double sum = 0, x, i, j, y, z=1, a, f=1, k=1;
    Step 3: Enter x // i.e. The range of sin series
    Step 4: Read x
    Step 5: Respect steps 6 to 11 for (i = 1 to i<=x)
    Step 6: Set j=z=1
    Step 7: Repeat steps 8 while (j<=i)
    Step 8: Set z=z*i; j=j+1;
    Step 9: Repeat steps 10 while (k <=i)
    Step 10: Set f=f*k; k=k+1;
    Step 11: Set a =z/f; sum=sum+a;
    Step 12: Display sum
    Step 13: Stop
```