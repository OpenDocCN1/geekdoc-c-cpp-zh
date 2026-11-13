![](bbox=[0.28, 0.08, 0.72, 0.21])

# Figure 11.26 Buffers required for k-way merge sort

k-Way merge sort requires k+1 buffers (Figure 11.26). A 2-way merge algorithm involves comparison strategy for two values which is easy to perform. One of the main problems in a general k-way merge is to establish an efficient comparison strategy that involves more than two values.

Consider the records in the k runs that are participating in the merge as players in the tournament. A competition tree can then be formed in which the winner of a particular competition is the record with the smallest key (Figure 11.27).

One typical tournament tree during the merging of k runs in a k-way merge is shown in Figure 11.27(a). The smallest key (first winner) for the above example is 2 and is placed in the output buffer. Similarly, the next smallest key (second winner) is to be found. In this case, it is 4. It should be noted that the record 2 is not considered for comparison (Figure 11.27(b)).

The third winner would be 5. In this case the buffer size is assumed to be of size 3 records. Once the buffer is full it is written to the disk. Once again the buffer is ready to receive the next 3 records. Since the contents of buffer is written to the disk once it is full, it requires only one buffer for the output where as k buffers are required for input.

A file consisting of 8 pages is sorted using 8-way merge sort (Figure 11.28). It took two passes to complete the sorting. During pass 1, tournament tree is used for merging. The 8-page run sorted output is shown in Figure 11.28. This output is on the disk.

The total cost for k-way merge sort is:

```
2N * (# of passes)
= 2N * [ceil(log_k N) + 1].
```

where N, is the number of pages in a file. If a file contains 8 pages, the total cost for a 2-way merge is = 2*8*4 = 64. If an 8-way merge is used the total cost is = 2*8*2 = 32. But the main memory buffer required by a 2-way merge is 11, whereas for 8-way merge is 9.

# Program 11.14

```
#include<iostream.h>
#include<conio.h>
void merge(int [],int,int);
void mergesort(int [],int,int);
int n,a[50],low,up,i,k;
void main()
{
clrscr();
cout<<"--------------------------";
cout<<"k-Way Merge Sort";
cout<<"n--------------------------";
```