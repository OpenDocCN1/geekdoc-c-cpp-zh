```
j=0;
for(i=0;i<k;i,j++)
   a[j++]=b[i];
for(i=n+1;i<=n;i++)
   a[j++]=a[i];
}
```

# Output

----------------------
K-way Merge Sort
----------------------
Enter K Value4
How Many Numbers You Want To Enter13
Enter Elements8
1
0
2
5
3
7
10
33
70
90
11
55
Before Sorting Record Elements Are
8 1 0 2 5 3 7 10 33 70 90 11 55
After Sorting Record Elements Are:
0 1 2 3 5 7 8 10 11 33 55 70 90

Program 11.4 sorts the given list of elements in ascending order using the k-way merge sort technique. The method merge() performs merging based on k-value and calls the mergesort() method which sorts the given list.