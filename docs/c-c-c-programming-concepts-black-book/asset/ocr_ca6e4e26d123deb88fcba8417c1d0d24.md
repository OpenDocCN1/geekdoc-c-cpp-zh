```
~~~c
L <- L.InsertLast(L2.Remove(L2.First()))
end
while(L1 != null)
begin
  L <- L.InsertLast(L1.Remove(L1.First()))
end
while(L2 != null)
begin
  L <- L.InsertLast(L2.Remove(L2.First()))
end
return L
end
~~~
```

In the preceding algorithm, first, the list is partitioned in such a way that at the end of the partition, there are a number of partitions, which is equal to the number of the list elements. By calling the MergeSort_Partition() function recursively, the list is partitioned. After the list is partitioned into single elements, the Merge() function is executed. In this function, we remove the smaller elements from L1 and L2 and place them immediately to the right of the earlier element in the resultant array. If this removal makes one list empty, then the remaining elements from the other lists are appended to the resultant list. This process is repeated until the entire list is sorted.

Now, let's analyze the merge sort algorithm. Among the family of divide and conquer sorting techniques, merge sort is the most efficient sorting algorithm, as its complexity even in the worst case is O(n log n). The reason behind this is that if a list is sorted in a reverse order, then

+   - O(log n) time is required to partition the list
+   - O(n) time is required to merge the two partitions

Therefore, the total complexity of the algorithm is O(n log n). In the best case, as the partitioning and merging will take place regardless of the order of the element, the complexity is O(n log n). Therefore, we can say that merge sort is useful, as it is fast regardless of the order of the elements as well as easy to understand and implement.

Listing 24.31 shows the implementation of merge sort in C:

Listing 31: Showing the Code for Merge Sort

```
~~~c
#include<stdio.h>
#include<conio.h>
void main()
{
 int size=1,l1,l2,k,aux[20],x[20],u1,u2,n,i,j;
 clrscr();
 printf("\n\t\tEnter the number of elements that is to be sorted");
 scanf("%d",&n);
 for(i=0;i<n;i++)
 {
  printf("\n\t\tEnter the a[%d]th element",i);
  scanf("%d",&x[i]);
 }
 while(size<n)
 {
  l1=0;
  k=0;
  while(l1+size<n)
  {
   l2=l1+size;
   u1=l2-1;
~~~
```