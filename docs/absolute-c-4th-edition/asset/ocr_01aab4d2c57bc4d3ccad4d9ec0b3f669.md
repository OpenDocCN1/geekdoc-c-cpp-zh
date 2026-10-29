# Display 5.8  Sorting an Array (part 3 of 3)

```
```cpp
51        v2 = temp;
52    }
53
54    int indexOfSmallest(const int a[], int startIndex, int numberUsed)
55    {
56        int min = a[startIndex];
57        indexOfMin = startIndex;
58        for (int index = startIndex + 1; index < numberUsed; index++)
59        {
60            if (a[index] < min)
61            {
62                min = a[index];
63                indexOfMin = index;
64                //min is the smallest of a[startIndex] through a[index]
65            }
66        return indexOfMin;
67    }
```
```

# SAMPLE DIALOGUE

> This program sorts numbers from lowest to highest.
> Enter up to 10 nonnegative whole numbers.
> Mark the end of the input with a negative number.
> 80 30 50 70 60 90 20 30 40 -1
> In sorted order the numbers are:
> 20 30 30 40 50 60 70 80 90

# Self-Test Exercises

+   17. Write a program that will read up to ten nonnegative integers into an array called `numberArray` and then write the integers back to the screen. For this exercise you need not use any functions. This is just a toy program and can be very minimal.
+   
+   18. Write a program that will read up to ten letters into an array and write the letters back to the screen in the reverse order. For example, if the input is
+   
+   `abcd.`
+   
+   then the output should be
+   
+   `dcba`