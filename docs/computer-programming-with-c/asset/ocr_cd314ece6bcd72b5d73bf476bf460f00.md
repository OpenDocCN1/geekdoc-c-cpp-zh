```
~~~
Enter the 5 elements
Enter element number 1
10
Enter element number 2
-2
Enter element number 3
-3
Enter element number 4
45
Enter element number 5
0
The positive count is 2
The negative count is 2
The zero count is 1
~~~
```

# **SCRATCH PAD**

+   - We create three different counters named as positive, negative and zero to store the counts of positive, negative and zero's present in the array. Initial value of all the counters is set to 0.
+   - We iterate over each element of the array using a for loop so as to determine if that element is a positive number, negative number or a zero.
+   - Depending on the type of element stored we increment the respective counter variable at each iteration of the for loop as shown in the code below:

```
~~~
for(i=0; i<=n-1; i++)
{
    if(a[i]>0)
    {
        positive++;
    }
    else if(a[i]<0)
    {
        negative++;
    }
    else
    {
        zero++;
    }
}
~~~
```

+   - At the end of loop, the variable positive will contain the count of positive numbers, negative will contain the count of negative numbers and the variable zero will contain count of zeros present in the array.

# **Solved Example 6.2**

Write a program to search a particular element in the array. The program should accept n integers as input from the user and store them in the array. The program should then accept a key x, and determine whether or not it is present in the array.