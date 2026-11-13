

## C 语言中的线性搜索程序

这里我们展示了C语言中线性搜索的实现。程序的输出在代码之后给出。

## 线性搜索程序

```
#include <stdio.h>
#define MAX 20
// array of items on which linear search will be conducted.
int intArray[MAX] = {1,2,3,4,6,7,9,11,12,14,15,16,17,19,33,34,43,45,55,66};
void printline(int count){
   int i;
   for(i = 0; i < count-1; i++){
      printf("=");
   }
   printf("=\n");
}
int find(int data){
   int comparisons = 0;
   int index = -1;
   int i;
   //navigate through all items
   for(i = 0; i < MAX; i++){
      // count the comparisons made
      comparisons++;
      // if data found, break the loop
      if(data == intArray[i]){
         index = i;
         break;
      }
   }
   printf("Total comparisons made: %d", comparisons);
   return index;
}
void display(){
   int i;
   printf("[");
   // navigate through all items
   for(i = 0; i < MAX; i++){
      printf("%d ", intArray[i]);
   }
   printf("]\n");
}
main(){
   printf("Input Array: ");
   display();
   printf("\n");
   //find location of 55
   int location = find(55);
   // if element was found
   if(location != -1)
      printf("\nElement found at location: %d", (location + 1));
   else
      printf("Element not found.");
}
```

如果编译并运行上面的程序，它将产生以下结果 -

```
Input Array: [1 2 3 4 6 7 9 11 12 14 15 16 17 19 33 34 43 45 55 66 ]

==================================================

Total comparisons made: 19

Element found at location: 19
```

## 17. 二分查找 数据结构与算法

二分查找是一种运行时间复杂度为 O(log n) 的快速搜索算法。该搜索算法基于分治原理。为了使该算法正常工作，数据集合应处于排序形式。

二分查找通过比较集合中间项来查找特定项。如果匹配，则返回项的索引。如果中间项大于该项，则在中间项右侧的子数组中搜索该项。否则，在中间项左侧的子数组中搜索该项。此过程在子数组上继续，直到子数组大小减为零。

## 二分查找的工作原理？

要使二分查找工作，目标数组必须已排序。我们将通过图示示例学习二分查找的过程。以下是我们的排序数组，假设我们需要使用二分查找查找值 31 的位置。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

首先，我们将使用公式 mid = low + (high - low) / 2 确定数组的一半。这里是 0 + (9 - 0) / 2 = 4（4.5 的整数值）。因此，4 是数组的中间位置。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

现在我们将位置 4 处存储的值与要搜索的值（即 31）进行比较。我们发现位置 4 处的值是 27，不匹配。由于该值大于 27 且我们有一个排序数组，因此我们也知道目标值必须在数组的上半部分。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

我们将 low 改为 mid + 1 并再次找到新的 mid 值。low = mid + 1 mid = low + (high - low) / 2 我们的新 mid 现在是 7。我们将位置 7 处存储的值与目标值 31 进行比较。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

位置 7 处存储的值不匹配，而是小于我们要查找的值。因此，该值必须从此位置的下半部分。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

因此，我们再次计算 mid。这次是 5。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

我们将位置 5 处存储的值与目标值进行比较。我们发现它是匹配的。

| 10 | 14 | 19 | 26 | 27 | 31 | 33 | 35 | 42 | 44 |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

我们得出结论，目标值 31 存储在位置 5。

二分查找将可搜索项目减半，从而将要进行的比较次数减少到非常少的数字。

## 伪代码

二分查找算法的伪代码应如下所示 –

```
Procedure binary_search A ← sorted array
n ← size of array
x ← value to be searched
Set lowerBound = 1 Set upperBound = n
while x not found
if upperBound < lowerBound EXIT: x does not exist.
set midPoint = lowerBound + ( upperBound - lowerBound ) / 2
if A[midPoint] < x
set lowerBound = midPoint + 1
if A[midPoint] > x
set upperBound = midPoint - 1
if A[midPoint] = x
EXIT: x found at location midPoint
end while
end procedure
```

要了解在C语言中使用数组实现二分查找，请单击此处。

## C 语言中的二分查找程序

二分查找是一种运行时间复杂度为 O(log n) 的快速搜索算法。该搜索算法基于分治原理。为了使该算法正常工作，数据集合应处于排序形式。

## C 语言实现

```
#include <stdio.h>
#define MAX 20
// array of items on which linear search will be conducted.
int intArray[MAX] = {1,2,3,4,6,7,9,11,12,14,15,16,17,19,33,34,43,45,55,66};
void printline(int count){
   int i;
   for(i = 0; i < count-1; i++){
      printf("=");
   }
   printf("=\n");
}
int find(int data){
   int lowerBound = 0;
   int upperBound = MAX - 1;
   int midPoint = -1;
   int comparisons = 0;
   int index = -1;
   while(lowerBound <= upperBound){
      printf("Comparison %d\n", (comparisons + 1));
      printf("lowerBound : %d, intArray[%d] = %d\n", lowerBound, lowerBound, intArray[lowerBound]);
      printf("upperBound : %d, intArray[%d] = %d\n", upperBound, upperBound, intArray[upperBound]);
      comparisons++;
      // compute the mid point
      midPoint = lowerBound + (upperBound - lowerBound) / 2;
      // data found
      if(intArray[midPoint] == data){
         index = midPoint;
         break;
      } else {
         // if data is larger
         if(intArray[midPoint] < data){
            // data is in upper half
            lowerBound = midPoint + 1;
         }
         // data is smaller
         else{
            // data is in lower half
            upperBound = midPoint - 1;
         }
      }
   }
   printf("Total comparisons made: %d", comparisons);
   return index;
}

void display(){
   int i;
   printf("\n");
   // navigate through all items
   for(i = 0; i < MAX; i++){
      printf("%d ", intArray[i]);
   }
   printf("\n");
}

main(){
   printf("Input Array: ");
   display();
   printline(50);
   // find location of 55
   int location = find(55);
   // if element was found
   if(location != -1)
      printf("\nElement found at location: %d", (location + 1));
   else
      printf("\nElement not found.");
}
```

如果编译并运行上面的程序，它将产生以下结果 -

```
Input Array: [ 1 2 3 4 6 7 9 11 12 14 15 16 17 19 33 34 43 45 55 66 ]
======================================================
Comparison 1
lowerBound : 0, intArray[0] = 1
upperBound : 19, intArray[19] = 66
Comparison 2
lowerBound : 10, intArray[10] = 15
upperBound : 19, intArray[19] = 66
Comparison 3
lowerBound : 15, intArray[15] = 34
upperBound : 19, intArray[19] = 66
Comparison 4
lowerBound : 18, intArray[18] = 55
upperBound : 19, intArray[19] = 66
Total comparisons made: 4
Element found at location: 19
```

