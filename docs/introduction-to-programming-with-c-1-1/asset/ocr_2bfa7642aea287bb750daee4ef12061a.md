```
}
}
if(found==1)
    printf("element found at %d position\n",i);
else
    printf("element not found\n");
getch();
}
```

Advantage:

+   - Very simple approach
+   - Works well for small arrays
+   - Used to search when the elements are not sorted

Disadvantage:

+   - Less efficient if the array size is large
+   - If the elements are already sorted, linear search is not efficient

**Binary search**: This technique can be applied if the array elements are sorted.

Working:

+   - Initialize position of the first element to variable low and position of last element to variable high. i.e., **low=0** and **high=n-1**
+   - Using above initial values obtain the position of middle element as **mid=(low+high)/2**
+   - The key to be searched is compared with middle element. If the key is same as middle element, then element found and stop searching process. If key is not same as middle element, it may be present in the left part or right part of the array.
+   - If key is less than the middle element, then left part of the array has to be compared from low to mid-1. So change upper bound as **high=mid-1**
+   - If key is greater than the middle element, then right part of the array has to be compared from mid+1 to high. So change lower bound as **low=mid+1**