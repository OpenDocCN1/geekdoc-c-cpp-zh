# 12 • Searching and Sorting Arrays 361

```
if(r <= 1)
    return;
  i = partition(a, 1, r);
  quick_sort(a, 1, i-1);
  quick_sort(a, i+1, r);
```

```
int partition(int a[], int 1, int r)
{
    int i, j, v, tmp;

    i = 1;
    j = r-1;
    v = a[r];
    while(1)
    {
        while(a[i] < v)
            i++;
        while(a[j] >= v)
        {
            if(j == 1) /* We check the case that the partition
element is the lower in the examined part. */
                break;
            
            if(i > j)
                break;
            tmp = a[i];
            a[i] = a[j];
            a[j] = tmp;
        }
    }
    tmp = a[i];
    a[i] = a[r];
    a[r] = tmp;
    return i;
```

**Comments:** See how the algorithms work, suppose the user enters the values: 2, 15, 4, 1, 7, 20, 25. Let's trace the first call of partition(). We have i-l=0, j-r=-5, v=a[6]=5. The first loop performs the left scan and terminates i becomes 1 (since a[1]>5). The second loop performs the right scan and terminates j becomes 3 (since a[3] < 5). The elements are swapped and the array is transformed to: 2, 1, 4, 15, 7, 20, 25.

Left scan continues until i becomes 3 (since a[3] > 5). Right scan continues and terminates j becomes 2 (since a[2] < 5). Because i > j the infinite loop terminates. a[3] and a[6] are swapped and the array is transformed to: 2, 1, 4, 5, 7, 20, 15. Notice that 5 is in its final position and for the right subarray (positions 4 to 6).

Before finishing this chapter, I'd like to note that the standard library provides many ready-to-algorithms (e.g., find()) it useful to have some experience in implementing algorithms by yourself. Not only because you may need knowledge either to write your own algorithms or standard code written by others, but also to get an idea about how they are implemented. For example, it is helpful for your programming expertise to know how a sorting algorithm is implemented just using the sort() function without having any idea. With the implementation examples of this chapter, I tried to give you this feeling of know-how.