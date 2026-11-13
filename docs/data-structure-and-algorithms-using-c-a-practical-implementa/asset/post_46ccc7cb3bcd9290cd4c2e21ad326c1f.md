
## PROGRAM FOR RADIX SORT

```cpp
#include<iostream>
using namespace std;
```

```cpp
//method to find the maximum value in the array
int maximum(int a[], int n)
{
	int max = a[0], i;
	for (i = 1; i < n; i++)
		if (a[i] > max)
			max = a[i];
	return max;
}
```

```cpp
void sort(int a[], int n, int exp)
{
	int out[n]; // output array
	int i, count[10] = {0};
	for (i = 0; i < n; i++)
		count[ (a[i]/exp)%10 ]++;

	for (i = 1; i < 10; i++)
		count[i] += count[i - 1];

	//construct the output array
	for (i = n - 1; i >= 0; i--)
	{
		out[count[ (a[i]/exp)%10 ] - 1] = a[i];
		count[ (a[i]/exp)%10 ]--;
	}

	for (i = 0; i < n; i++)
		a[i] = out[i];
}
```

```cpp
void radix(int a[], int n)
{
	// Find the maximum number to know number of digits
	int m = maximum(a, n);
	for (int exp = 1; m/exp > 0; exp *= 10)
		sort(a, n, exp);
}
```

```cpp
void print(int a[], int n)
{
 for (int i = 0; i < n; i++)
  cout << a[i] << " ";
}
```

```cpp
int main()
{
 int n,*arr,i;
 cout<<endl<<"Input the number of elements in the list:";
 cin>>n;
 arr = new int[n];
 for(i = 0 ; i < n ; i++)
 {
  cout<<endl<<"Enter a number";
  cin>>arr[i];
 }
 radix(arr, n);
 print(arr, n);
 return 0;
}
```

## OUTPUT

![](img/1faaa0256577c74e8a61f42967760aa8_376_0.png)

## 10.9 Heap Sort

Heaps are based on the concept of a complete tree. Formally a binary tree is completely full if it is of height h and has 2^(h+1) - 1 nodes. A binary tree of height h is complete if

- 1. it is empty or
- 2. Its left subtree is complete of height h – 1 and its right subtree is completely full of height h – 2 or
- 3. its left subtree is completely full of height h – 1 and its right subtree is complete of height h – 1.

A binary tree has the heap property if

- 1. It is empty or
- 2. The key in the root is larger than that in either child and both subtrees have the heap property.

A heap can be used as priority queue: the highest priority item is at the root and is trivially extracted. But if the root is deleted, we are left with two sub-trees and we must efficiently re-create a single tree with the heap property. The value of the heap structure is that we can both extract the highest priority item and insert a new one in O(logn) time.

A heap is an ordered balanced binary tree (complete binary tree) in which the value of the node at the root of any sub-tree is less than or equals to the value of either of its children.

## ALGORITHM

- Step-1 Create a heap
- Step-2 [do sorting]
- Repeat through step-10 for k = n to 2
- Step-3 list[1] = list[k]
- Step-4 temp = list[1]
- I=1
- J=2
- Step-5 [find the index of largest child of new element]
- If j+1<k then
- If list[j+1] > list[j]
- Then j=j+1
- Step-6 Construct the new heap
- Step-7 Repeat through step-10 while j<=k-1 and list[j]>temp
- Step-8 Interchange elements List[I] = list[j]
- Step-8 Obtain left child
- I=j
- J=2*I
- Step-9 [Obtain the index of next largest child]
- If j+1<k
- If list[j+1] > list[j] then j=j+1
- Else
- If j>n then j=1
- Step-10 [Copy elements into its proper place]
- List[j] = temp
- Step-11 exit

## /*PROGRAM FOR HEAP SORT*/

```cpp
#include<iostream>
#include<conio.h>
using namespace std;
void heap(int *, int );
void create(int *, int);
void display(int *, int);

int main()
{
 int arr[100];
 int i, size;
 cout<<endl<<"Enter number of elements";
 cin>>size;
 cout<<"\nSize of the list: "<<size;
 for(i = 1 ; i <= size ; ++i)
 {
  cout<<"\nEnter a number";
  cin>>arr[i];
 }
 cout<<"\nEntered list is as follows:\n";
 display(arr, size);
 create(arr, size);
 cout<<"\nHeap tree is\n";
 display(arr, size);
 cout<<endl<<endl;
 heap(arr,size);
 cout<<"\n\n Sorted list is as follows :\n\n";
 display(arr,size);
}
void create(int list[], int n )
{
 int k, j, i, temp;
 for(k = 2 ; k < n; ++k)
 {
     i = k ;
     temp = list[k] ;
     j = i / 2 ;
     while((i > 1) && (temp > list[j]))
     {
         list[i] = list[j] ;
         i = j ;
         j = i / 2 ;
         if ( j < 1 )
             j = 1 ;
     }
     list[i] = temp ;
 }
}
```

```cpp
void heap(int arr[], int n)
{
    int k, temp, value, j, i, p;
    int step = 1;
    for(k = n ; k >= 2; --k)
    {
        temp = arr[1] ;
        arr[1] = arr[k] ;
        arr[k] = temp ;

        i = 1 ;
        value = arr[1];
        j = 2 ;

        if((j+1 < k))
        {
            if(arr[j+1] > arr[j])
                j ++;
        }
        while((j <= k) && (arr[j] > value))
        {
            arr[i] = arr[j];
            i = j ;
            j = 2*i ;
            if((j+1) < k)
            {
                if(arr[j+1] > arr[j])
                    j++;
            }
            else
                if ( j > n)
                    j = n ;
        }
        arr[i] = value;
    }
    cout<<"\n Step = "<<step;
    step++;
    for(p = 1; p < n; p++)
        cout<<setw(5)<<arr[p];
}
void display(int arr[], int n)
{
int i;
for(i = 1 ; i <= n; ++ i)
{
cout<<setw(5)<<arr[i];
}
}
```

## OUTPUT

```
Enter number of elements?
Size of the list:
Enter a number:25
Enter a number62
Enter a number8
Enter a number93
Enter a number5
Enter a number:
Enter a number45
Entered list is as follows:
25 62 8 93 5 7 45
Heap tree is
93 62 45 25 5 7 8
Step = 1 62 25 45 5 8 5 7 93
Step = 2 45 25 7 7 8 5 62 93
Step = 3 25 5 8 7 5 45 62 93
Step = 4 8 5 5 7 25 45 62 93
Step = 5 7 5 8 25 45 62 93
Step = 6 5 7 8 25 45 62 93
Sorted list is as follows :
5 7 8 25 45 62 93
Process exited after 9.935 seconds with return value 0
Press any key to continue . . .
```

| SORTING TECHNIQUE | BEST CASE | AVERAGE CASE | WORST CASE |
|---|---|---|---|
| Bubble | O(n) | O(n²) | O(n²) |
| Insertion | O(n) | O(n²) | O(n²) |
| Selection | O(n²) | O(n²) | O(n²) |
| Quick | O(n²) | O(n logn) | O(n²) |
| Merge | O(n logn) | O(n logn) | O(n logn) |
| Radix | O(n²) | O(n logn) | O(n logn) |
| Heap | O(n logn) | O(n logn) | O(n logn) |

## COMPARISON BETWEEN THE SORTING PROGRAMS

```cpp
#include<iostream>
#include <ctime>
#include <stdlib.h>
void adjust(int );
void heapify(int);
void swap(long int &, long int &);
int partition(int,int);
void quickSort(int,int);
void merge(int l, int m, int r);
void mergesort(int l, int r);
using namespace std;
long int *a;
int n;
void swap(long int* a, long int* b)
{
 long int t = *a;
 *a = *b;
 *b = t;
}
//selection sort
void selection(int n)
{
 int i,j;
 long int t;
 //logic to sort the array of elements
 for(i=0;i<n;i++)
 {
 for(j=1+r;j<n;j++)
 {
  if(a[i]>a[j])
  {
  //swap the numbers
  t=a[i];
  a[i]=a[j];
  a[j]=t;
  }
 }
 }
}

//method to generate n random numbers and store it into array
void input(int n)
{
int i;
int timetaken[5] [6];
a = new long int[n];//allocate memory for n number of
elements
for(i=0;i<n;i++)
{ //generate the numbers and assign to array
a[i] = rand() % 10000 + 1;
}
}

//heapsort() method
void heapsort(int n)
{
int i,t;
heapify(n); //call to heapify method
for(i=n-1;i>=0;i--)
{ t = a[0]; //perform swap operation
a[0] = a[i];
a[i] = t;
adjust(i);
}
}

//heapify() method
void heapify(int n) {
int k,i,j,item;
for (k=1;k<=n;k++) {
item = a[k];
i = k;
j = (i-1)/2;
while ((i>0)&&(item>a[j])) {
a[i] = a[j];
i = j;
j = (i-1)/2;
}
a[i] = item;
}
}
```

```cpp
//adjust() method
void adjust(int n) {
    int i,j,item;
    j = 0;
    item = a[j];
    i = 2*j+1;
    while(i<=n-1) {
        if(i+1 < n-1)
            if(a[i] < a[i+1])
                i++;
        if(item<a[i]) {
            a[j] = a[i];
            j = i;
            i = 2*j+1;
            else
                break;
        }
        a[j] = item;
    }
}
```

```cpp
//quick sort
int partition(int low, int high)
{
    long int pivot = a[high];     //assign the pivot element
    int i = (low - 1);
    for (int j = low; j <= high-1; j++)
    {
        if (a[j] <= pivot)
        {
            i++;     // increment index of smaller element
            swap(&a[i], &a[j]);
        }
    }
    swap(&a[i + 1], &a[high]);
    return (i + 1);
}
```

```cpp
void quicksort( int low, int high)
{
    if (low < high)
    {
        int pi = partition(low, high) ;
```
