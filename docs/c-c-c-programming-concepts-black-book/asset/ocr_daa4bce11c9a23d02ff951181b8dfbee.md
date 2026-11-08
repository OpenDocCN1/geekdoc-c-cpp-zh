```
```cpp
}
}
int quick(int left,int right)
{
    T t;
    int pos;
    pos=left;
    while(left<=right)
    {
        while(a[pos]<=a[right] && pos!=right)
            right=right-1;
        if(pos==right)
            return pos;
        t=a[pos];
        a[pos]=a[right];
        a[right]=t;
        pos=right;
        while(a[pos]>=a[left]&&pos!=left)
            left++;
        if(pos==left)
            return pos;
        t=a[pos];
        a[pos]=a[left];
        a[left]=t;
        pos=left;
    }
}
};
void main(void)
{
    qsort <int> q;
    clrscr();
    q.getdata();
    cout<<endl<<endl<<" Your entered sequence:-> ";
    q.display();
    q.quicksort();
    cout<<endl<<endl<<" Sorted sequence:-> ";
    q.display();
    getch();
}
```
```

# Merge Sort

Merge sort is another sorting technique that is based on the divide and conquer strategy. In the divide step, it divides the array into two halves of the same size. In the conquer step, the two sub-arrays are conquered by recursively applying the sorting technique. At the end of the process, the already sorted sub-arrays are merged until they get back to the original size of the initial array. In this way, the sorted array is achieved.

As the merge sort follows the three steps of divide and conquer paradigm, we can represent the merge sort technique as follows:

+   1. Divide the array A[n] into two halves.
+   2. Continue division until there is a single element left, which is sorted by its own.
+   3. Merge already sorted sub-arrays into one and continue merging until the actual length of the array is reached. This process will result in a sorted array.