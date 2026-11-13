```
else if (arr[mid]>num)
    end = mid-1;
else
    beg = mid+1;
}
if (beg > end && found == 0)
    printf("\n %d does not exist in the array", num);
return 0;
}
int smallest(int arr[], int k, int n)
{
    int pos = k, small=arr[k], i;
    for(;k<=i+1;n++;)
    {
        if(arr[i]< small)
        {
            small = arr[i];
            pos = i;
        }
    }
    return pos;
}
void selection_sort(int arr[], int n)
{
    int k, pos, temp;
    for(k=0;k<n;k++)
    {
        pos = smallest(arr, k, n);
        temp = arr[k];
        arr[k] = arr[pos];
        arr[pos] = temp;
    }
}
```

# 14.4 INTERPOLATION SEARCH

Interpolation search, also known as extrapolation search, is a searching technique that finds a

specified value in a sorted array. The concept of interpolation search is similar to how we search for names in a telephone book or for keys by which a book's entries are ordered. For example, when looking for a name “Bharat” in a telephone directory, we know that it will be near the extreme left, so applying a binary search technique by dividing the list in two halves each time is not a good idea. We must start scanning the extreme left in the first pass itself.

![](bbox=[0.1, 0.58, 0.56, 0.9])

Figure 14.3 Algorithm for interpolation search

In each step of interpolation search, the remaining search space for the value to be found is calculated. The calculation is done based on the values at the bounds of the search space and the value to be searched. The value found at this estimated position is then compared with the value being searched for. If the two values are equal, then the search is complete.