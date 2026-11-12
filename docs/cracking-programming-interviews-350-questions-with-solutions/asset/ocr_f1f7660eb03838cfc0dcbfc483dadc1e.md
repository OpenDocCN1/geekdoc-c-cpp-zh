```
~~~c
if (value < sorted_array[l] || value >
    sorted_array[r])
{
    position = 0;
}
else
{
    position = interpolation_search_helper(
        sorted_array, l, r, value);
}
return position;
}

int main()
{
    int sorted_array[] = {1, 2, 3, 4, 5, 6, 7, 8,
        9};

    assert(interpolation_search(sorted_array, 0, 8,
        5) == 4);
}
~~~
```

# ### Remarks

For external search (the file resides on an external device), interpolation search is superior to binary search since the search time is determined by the number of accesses. However, in internal search the computation time of each iteration should also be considered. Computer experiments showed that interpolation search and binary search take approximately the same time. Interpolation search is slightly faster only for files larger than 5000 records. However, using shift operations instead of division in binary search or the use of Fibonacci search results in faster internal search methods. After a few iterations of interpolation search, we are quite close to the required record. When the difference between the indices of two successive iterations is small, it may be advantageous to switch to sequential search and save computation time.

# ## 2.7 Robot Walk

# ### Problem Description

Given are two integer arrays $x[0..46]$ and $y[0..46]$. The pair $(x[i], y[i])$ represents the Cartesian coordinates of a point $P_i$ in a plane ($0 ≤ i < 47$). The arrays are such that all 47 points are different.

A robot walks from $P_0$ to $P_1$, from $P_1$ to $P_2$, ..., from $P_{45}$ to $P_{46}$, and finally from $P_{46}$ to $P_0$. It does so in obedience to the following rules:

+   - it shall start from $P_0$, while looking towards $P_1$