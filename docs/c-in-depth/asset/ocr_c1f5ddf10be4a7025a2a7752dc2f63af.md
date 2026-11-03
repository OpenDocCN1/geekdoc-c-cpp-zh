```
{
    if(arr[i]>arr[j])
    {
        temp=arr[i];
        arr[i]=arr[j];
        arr[j]=temp;
    }
}
printf("Sorted array is : \n");
for(i=0;i<SIZE;i++)
    printf("%d ",arr[i]);
printf("\n");
}
```

# Problem 4

Write a program to sort the elements of a 1-D array, in ascending order through bubble sort If N elements are given, then the procedure for sorting them through bubble sort is as- The elements of array are arr[0],arr[1],....................arr[N-1]

# Pass 1:

+   - Compare 0th and 1st element, If 0th >1st then exchange them
+   - Compare 1st and 2nd element, If 1st > 2nd then exchange them,
+   - Compare 2nd and 3rd element, If 2nd > 3rd then exchange them,
+   - Compare N-2th with N-1th , If N-2th > N-1th then exchange them

# Pass 2:

+   - Compare 0th and 1st element, If 0th >1st then exchange them
+   - Compare 1st and 2nd element, If 1st > 2nd then exchange them,
+   - Compare 2nd and 3rd element, If 2nd > 3rd then exchange them,
+   - Compare N-3th and N-2th element, If N-3th > N-2th then exchange them

# Pass N-1:

Compare 0th and 1st element, If 0th >1st then exchange them
Let us take a list of elements in unsorted order and sort them by applying bubble sort.
Elements of the array are-
40 20 50 60 30 10