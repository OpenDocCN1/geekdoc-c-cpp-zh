
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | ... |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

Searching can start from somewhere middle in the list rather than from the beginning to optimize performance.

We can also improve the performance of jump search algorithm by repeatedly applying jump search. For example, if the size of the list is 10,00,000 (n). The jump interval would then be √n = √1000000 = 1000. Now, even the identified interval has 1000 elements and is again a large list. So, jump search can be applied again with a new step size of √1000 ≈ 31. Thus, every time we have a desired interval with a large number of values, the jump search algorithm can be applied again but with a smaller step. However, in this case, the complexity of the algorithm will no longer be O(n/√n) but will approach a logarithmic value.

## Complexity of Jump Search Algorithm

Jump search works by jumping through the array with a step size (optimally chosen to be √n) to find the interval of the value. Once this interval is identified, the value is searched using the linear search technique. Therefore, the complexity of the jump search algorithm can be given as O(√n).

### PROGRAMMING EXAMPLE

- 4. Write a program to search an element in an array using jump search.

```c
#include <stdio.h>
#include <math.h>
#include <conio.h>
#define MAX 20
int jump_search(int a[], int low, int high, int val, int n)
{
	int step, i;
	step = sqrt(n);
	for(i=0;i<step;i++)
	{
		if(val < a[step])
		{
			high = step - 1;
		}
		else
		low = step + 1;
	}
	for(i=low;i<=high;i++)
	{
		if(a[i]==val)
			return i;
	}
	return -1;
}

int main()
{
	int arr[MAX], i, n, val, pos;
	clrscr();
	printf("\n Enter the number of elements in the array : ");
	scanf("%d", &n);
	printf("\n Enter the elements : ");
	for(i = 0; i < n; i++)
		scanf("%d", &arr[i]);
	printf("\n Enter the value to be searched : ");
	scanf("%d", &val);
	pos = jump_search(arr, 0, n-1, val, n);
	if(pos == -1)
	 printf("\n %d is not found in the array", val);
	 else
	 printf("\n %d is found at position %d", val, pos);
	 getche();
	 return 0;
 }
```

## Fibonacci Search

We are all well aware of the Fibonacci series in which the first two terms are 0 and 1 and then each successive term is the sum of previous two terms. In the Fibonacci series given below, each number is called a Fibonacci number.
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

The same series and concept can be used to search for a given value in a list of numbers. Such a search algorithm which is based on Fibonacci numbers is called Fibonacci search and was developed by Kiefer in 1953. The search follows a divide-and-conquer technique and narrows down possible locations with the help of Fibonacci numbers.
Fibonacci search is similar to binary search. It also works on a sorted list and has a run time complexity of O(log n). However, unlike the binary search algorithm, Fibonacci search does not divide the list into two equal halves rather it subtracts a Fibonacci number from the index to reduce the size of the list to be searched. So, the key advantage of Fibonacci search over binary search is that comparison dispersion is low.

## 14.6 INTRODUCTION TO SORTING

Sorting means arranging the elements of an array so that they are placed in some relevant order which may be either ascending or descending. That is, if A is an array, then the elements of A are arranged in a sorted order (ascending order) in such a way that A[0] < A[1] < A[2] < ..... < A[N].
For example, if we have an array that is declared and initialized as
int A[] = {21, 34, 11, 9, 1, 0, 22};
Then the sorted array (ascending order) can be given as:
A[] = {0, 1, 9, 11, 21, 22, 34};

A sorting algorithm is defined as an algorithm that puts the elements of a list in a certain order, which can be either numerical order, lexicographical order, or any user-defined order. Efficient sorting algorithms are widely used to optimize the use of other algorithms like search and merge algorithms which require sorted lists to work correctly. There are two types of sorting:

- Internal sorting which deals with sorting the data stored in the computer’s memory.
- External sorting which deals with sorting the data stored in files. External sorting is applied when there is voluminous data that cannot be stored in the memory.

### 14.6.1 Sorting on Multiple Keys

Many a times, when performing real-world applications, it is desired to sort arrays of records using multiple keys. This situation usually occurs when a single key is not sufficient to uniquely identify a record. For example, in a big organization we may want to sort a list of employees on the basis of their departments first and then according to their names in alphabetical order.
Other examples of sorting on multiple keys can be

- Telephone directories in which names are sorted by location, category (business or residential), and then in an alphabetical order.
- In a library, the information about books can be sorted alphabetically based on titles and then by authors' names.
- Customers' addresses can be sorted based on the name of the city and then the street.

**Note** Data records can be sorted based on a property. Such a component or property is called a sort key. A sort key can be defined using two or more sort keys. In such a case, the first key is called the primary sort key, the second is known as the secondary sort key, etc.

Consider the data records given below:

| Name | Department | Salary | Phone Number |
| :--- | :--- | :--- | :--- |
| Janak | Telecommunications | 1000000 | 9812345678 |
| Raj | Computer Science | 890000 | 9910023456 |
| Aditya | Electronics | 900000 | 7839897654 |
| Huma | Telecommunications | 1100000 | 9654123456 |
| Divya | Computer Science | 750000 | 9350123455 |

Now if we take department as the primary key and name as the secondary key, then the sorted order of records can be given as:

| Name | Department | Salary | Phone Number |
| :--- | :--- | :--- | :--- |
| Divya | Computer Science | 750000 | 9350123455 |
| Raj | Computer Science | 890000 | 9910023456 |
| Aditya | Electronics | 900000 | 7839897654 |
| Huma | Telecommunications | 1100000 | 9654123456 |
| Janak | Telecommunications | 1000000 | 9812345678 |

Observe that the records are sorted based on department. However, within each department the records are sorted alphabetically based on the names of the employees.

### 14.6.2 Practical Considerations for Internal Sorting

As mentioned above, records can be sorted either in ascending or descending order based on a field often called as the sort key. The list of records can be either stored in a contiguous and randomly accessible data structure (array) or may be stored in a dispersed and only sequentially accessible data structure like a linked list. But irrespective of the underlying data structure used to store the records, the logic to sort the records will be same and only the implementation details will differ.

When analysing the performance of different sorting algorithms, the practical considerations would be the following:

- Number of sort key comparisons that will be performed
- Number of times the records in the list will be moved
- Best case performance
- Worst case performance
- Average case performance
- Stability of the sorting algorithm where stability means that equivalent elements or records retain their relative positions even after sorting is done

## 14.7 BUBBLE SORT

Bubble sort is a very simple method that sorts the array elements by repeatedly moving the largest element to the highest index position of the array segment (in case of arranging elements in ascending order). In bubble sorting, consecutive adjacent pairs of elements in the array are compared, with each other. If the element at the lower index is greater than the element at the higher index, the two elements are interchanged so that the element is placed before the bigger one. This process will continue till the list of unsorted elements exhausts. This procedure of sorting is called bubble sorting because elements ‘bubble’ to the top of the list. Note that at the end of the first pass, the largest element in the list will be placed at its proper position (i.e., at the end of the list).

> Note If the elements are to be sorted in descending order, then in first pass the smallest element is moved to the highest index of the array.

### Technique

The basic methodology of the working of bubble sort is given as follows:

- (a) In Pass 1, A[0] and A[1] are compared, then A[1] is compared with A[2], A[2] is compared with A[3], and so on. Finally, A[N-2] is compared with A[N-1]. Pass 1 involves n-1 comparisons and places the biggest element at the highest index of the array.
- (b) In Pass 2, A[0] and A[1] are compared, then A[1] is compared with A[2], A[2] is compared with A[3], and so on. Finally, A[N-3] is compared with A[N-2]. Pass 2 involves n-2 comparisons and places the second biggest element at the second highest index of the array.
- (c) In Pass 3, A[0] and A[1] are compared, then A[1] is compared with A[2], A[2] is compared with A[3], and so on. Finally, A[N-4] is compared with A[N-3]. Pass 3 involves n-3 comparisons and places the third biggest element at the third highest index of the array.
- (d) In Pass n-1, A[0] and A[1] are compared so that A[0] < A[1]. After this step, all the elements of the array are arranged in ascending order.

### Example 14.2 To discuss bubble sort in detail, let us consider an array A[] that has the following elements:

```
A[] = {30, 52, 29, 87, 63, 27, 19, 54}
```

- Pass 1:
- (a) Compare 30 and 52. Since 30 < 52, no swapping is done.
- (b) Compare 52 and 29. Since 52 > 29, swapping is done.
- 30, 29, 52, 87, 63, 27, 19, 54
- (c) Compare 52 and 87. Since 52 < 87, no swapping is done.
- (d) Compare 87 and 63. Since 87 > 63, swapping is done.
- 30, 29, 52, 63, 87, 27, 19, 54
- (e) Compare 87 and 27. Since 87 > 27, swapping is done.
- 30, 29, 52, 63, 27, 87, 19, 54
- (f) Compare 87 and 19. Since 87 > 19, swapping is done.
- 30, 29, 52, 63, 27, 19, 87, 54
- (g) Compare 87 and 54. Since 87 > 54, swapping is done.
- 30, 29, 52, 63, 27, 19, 54, 87

Observe that after the end of the first pass, the largest element is placed at the highest index of the array. All the other elements are still unsorted.

- Pass 2:
- (a) Compare 30 and 29. Since 30 > 29, swapping is done.
- 29, 30, 52, 63, 27, 19, 54, 87
- (b) Compare 30 and 52. Since 30 < 52, no swapping is done.
- (c) Compare 52 and 63. Since 52 < 63, no swapping is done.
- (d) Compare 63 and 27. Since 63 > 27, swapping is done.
- 29, 30, 52, 27, 63, 19, 54, 87
- (e) Compare 63 and 19. Since 63 > 19, swapping is done.
