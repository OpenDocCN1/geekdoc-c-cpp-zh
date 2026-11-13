
## Program 16.10

```cpp
/*To search an element in the given list using Binary search*/
#include<iostream.h>
#include<conio.h>
void sort(int a[],int n)
{
 int i,j;
 for(i=n-1;i>=0;i--)
  for(j=0;j<i;j++)
   if(a[j]>a[j+1])
   {
    a[j]=(a[j]+a[j+1])-(a[j+1]=a[j]);
   }
}
void main()
{
 int i,a[30],n,low,up,search,mid;
 clrscr();
 cout<<"Enter Size Of Array:";
 cin>>n;
 cout<<"Enter "<<n<<"Elements:";
 for(i=0;i<n;i++)
  cin>>a[i];
 cout<<"Enter Search Element:";
 cin>>search;
 sort(a,n);
 low=0,up=n-1;
 while(low<=up)
 {
  mid=(low+up)/2;
  if(a[mid]==search)
  {
   cout<<"Search Element"<<search<<"Is Found At"<<mid+1<<"Location";
   getch();
   return;
  }
  else if(a[mid]>search)
   up=mid-1;
  else
   low=mid+1;
 }
 cout<<"Search Element"<<search<<"Is Not Found";
 getch();
}
```

### Output

Enter Size Of Array:7
Enter 7 Elements:8
4
0
6
9
2
1
Enter Search Element :6
Enter Element 6 Is Found At 5 Location

## 16.2.3 Fibonacci Search

The Fibonacci search is a technique of searching a sorted array using the divide and conquer principle that narrows down possible locations with the use of Fibonacci numbers. Compared to binary search, Fibonacci search finds the locations whose addresses have lower distribution. The advantage of Fibonacci search over binary search is that it slightly reduces the average time needed to access a storage location.

Fibonacci search has a complexity of O(log(n)). Instead of splitting the array in the middle, this implementation splits the array corresponding to the Fibonacci numbers, which are defined by the following recurrence relations:

```
F_0 = 0
F_1 = 1
F_2 = 1
F_n = F_{n-1} + F_{n-2}, for n>=2
```

Fibonacci sequence when used as a search technique is termed as Fibonacci search. As the binary search determines the median in the new list as the next element for comparison, the Fibonacci search also determines the next element for comparison, which is indicated by the sequence of Fibonacci number. Fibonacci search performs search technique only on the ordered list. For the convenience of explanation, consider that the number of lists is one less than the Fibonacci number, i.e. n=F_{n-1}.

Consider an ancestor, parent and its child nodes to perform Fibonacci search on a decision tree that satisfies the following properties. If the difference in index between parent and ancestor is F_p, then

- i. If the parent is a left child node, then the difference between parent and its child in an index is F_{p-1}.
- ii. If the parent is a right child node, then the difference between parent and its child in the index is F_{p-2}.

Suppose consider an order list L = {E_1, E_2, E_3, ..., E_n}, where n is F_{k-1}. The Fibonacci search decision tree is shown in Figure 16.12. For n=20 where 20=F_{k-1}, the root of the decision tree which is the first element to be compared with the element ITEM is E_i, whose index i is the closest Fibonacci number to n. Here for n=20, 13 is the closest Fibonacci sequence number. So, E_i is the root.

If Item<E_i, then the next element to be compared is E_i. If Item>E_i, then the next element to be compared is E_a and so on. By the above properties, the other decision nodes can be easily determined. The right child of E_i should be E_a and for E_a the right child should be E_b, and so on.

Consider the nodes E_a and E_b and E_c, since E_a is the right child of E_b, the difference between them is 3, i.e. F_p (because F_p=F_{p-1}+F_3). The difference between E_a and its two children is F_q which is 1. Hence the two child nodes of E_a are E_a and E_b. Similarly consider the nodes E_a and E_b, is the left child of E_a and the difference between them is given by F_q, the two child nodes of E_a are given by E_a and E_b, their difference is F_q.

Algorithm 16.11 is the algorithm for Fibonacci search. Here DATA is an ordered list and n is the number of elements such that F_{k-1} > (n+1) and F_{k-2} = (n+1). Item is the one to be searched in the list.

### Figure 16.12 Fibonacci search decision tree

![](img/45784b9f0334626143002ec0d63692fd_566_0.png)

### Algorithm 16.11: FIBONACCI SEARCH (DATA, n, ITEM)

- 1. Set p=Fk-1, q=Fk-2, r=Fk-3 and M=(n+1)-(p+q) ; //Obtain the largest Fibonacci number FK close to n+1.
- 2. Check whether ITEM is greater than DATA [p] then
  - Set flag=false;
  - Set p=p+m;
  - Set flag=false;
- 3. loop while (p!=0 and flag=true)
  1. Check whether ITEM=DATA [p] then
     Print "successful search";
  2. Check whether ITEM<DATA [p] then
     If (x=0) then set p to 0
     Else
     Set p=p-r, t=q, q=r and r=t-r;
  3. Check whether ITEM>DATA [p] then
     If (q=1) then Set p=0
     Else
     Set p=p+r, q=q-r and r=r-q
  4. End
- 4. End loop
- 5. Check whether flag=true then
  Print "search is unsuccessful");
- 6. End.

### Example 16.13

The Fibonacci search algorithm can be easily understood by tracing the algorithm. The trace of Fibonacci search is shown in Figure 16.13. Here, the array DATA contains 20 elements such that F7(n+1) + F6(m=n+1) where m=0 and n=20. Let search for the element K=100 in the list {10,15,20,25,30,35,40,45,50,55,60,65,70,75,80,85,90,95,100,105}.

The algorithm for Fibonacci search first gets the largest number closer to n+1, i.e. in this case it is F7. Compare K=100 with the data element with index F7, that is DATA[13]=70. Since K>DATA[13], the list is reduced to DATA[14:20]={75,80,85,90,95,100,105}. Now compare K with DATA[18]=95, since K>DATA[18], the list is further reduced to DATA[19:20]={100,105}. Again compare K with DATA[20], since K<DATA[20] reduce the list to DATA[20:20]={100} which when searched again contains the search element. The element is searched successfully.

| Searching element | Check K, DATA[P] | p,q,r,t values | |
|---|---|---|---|
| K=100 | | p=13,q=8,r=5 | n=0, m=0 since F7+0=n+1 |
| | K>DATA[13]=70 | p=13,q=8,r=5 | p=p+m since K>DATA[p] |
| | | p=18,q=3,r=2 | |
| | K>DATA[18]=95 | p=20,q=1,r=1,t=1 | |
| | K=DATA[20]=105 | p=19,q=1,r=0 | |
| | K=DATA[19]=100 | | Element found |

![](img/45784b9f0334626143002ec0d63692fd_567_0.png)

Complexity: The time complexity is measured in terms of the number of comparisons taken to locate ITEM in DATA which contains n elements. Since each comparison reduces the array size in half, f(n) comparisons are required to locate ITEM where 2f(n)>n or f(n)=log n+1

### Limitations:

- 1. List must be already sorted.
- 2. Direct access to the middle element in any sublist is done that requires a sorted array to hold the data, which will be very expensive when there are many insertions and deletions.

## Program 16.11

```cpp
#include<iostream.h>
#include<conio.h>
void sort (int a[],int n)
{
int i,j;
for(i=n-1;i>0;i--)
for(j=0;j<i;j++)
if(a[j]>a[j+1])
a[j]=a[j]+a[j+1]-(a[j+1]=a[j]) ;
}
int fib(int c)
{
 int f1=-1,f2=1,f3;
 while (f2<=c)
 {
 f3=f1+f2, f1=f2, f2=f3;
 if (f3==c)
 return f3;
 if (f3<c)
 return f1;
 }
 return 0;
}
void fsearch(int a[],int x,int y,int s)
{
 while(x<y)
 {
 int count=0,cl=1,flag=0,i,mid;
 for(i=x;i<y;i++)
 count++;
 mid=fib(count);
 for(i=x;i<y&&(cl==1);i++)
 {
 flag++;
 if(flag==mid)
 mid=x,cl=0;
 }
 if(a[mid]==s)
 {
 cout<<"Search Element "<<s<<" Is Found";
 getch();
 return;
 }
 if(a[mid]>s)
 y=mid-1;
 else
 x=mid+1;
 }
 cout<<"Search Element "<<s<<" Is Not Found";
}
void main()
{
 int i,a[30],n,search;
 clrscr();
 cout<<"Enter Size Of Array:";
 cin>>n;
 cout<<"Enter "<<n<<" Elements:";
 for(i=0;i<n;i++)
 cin>>a[i];
 cout<<"Enter Search Element :";
 cin>>search;
 sort(a,n);
 fsearch(a,0,n,search);
}
```

### Output

Enter Size Of Array:10
Enter 10 Elements:4 2 6 3 1 5 7 8 10 21
Enter Search Element :8
Search Element 8 Is Found

Enter Size Of Array:5
Enter 5 Elements:6
2
4
3
7
Enter Search Element:10
Search Element 10 Is Not Found

## SUMMARY

- The bubble sort works by iterating down an array to be sorted from the first element to the last, comparing each pair of elements and switching their positions if necessary.
- Insertion sort inserts each element of the array into its proper position leaving progressively larger stretches of the array sorted.
- Quicksort is a relatively simple sorting technique using the divide-and-conquer recursive procedure.
- Merge sort is a fast, stable sorting routine with guaranteed O(n log n) efficiency.
- The idea of Shell sort is to arrange the data sequence in a two-dimensional array and sort the columns of the array.
- Radix sort keeps the elements in order by comparing the digits of the numbers.
- Heap sort is a relatively simple technique built upon the heap data structure.
- Searching is the process of finding the location of a given element in a set of elements.
- Linear is the technique of searching a given item in the list by comparing each and every element in the list sequentially.
- Binary search is a technique of searching an item in the ordered list by dividing the list into two halves with each comparison until the item is found or not.
- The Fibonacci search is a technique of searching a sorted array using the divide and conquer principle.
- Fibonacci search determines the next element for comparison based on the sequence of the Fibonacci number and it performs a search technique only on the ordered list.
