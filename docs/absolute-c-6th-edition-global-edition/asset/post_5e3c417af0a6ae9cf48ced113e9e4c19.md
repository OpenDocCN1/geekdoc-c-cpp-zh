
## EXAMPLE: (continued)

One way to design an algorithm is to rely on the definition of the problem. In this case the problem is to sort an array a from smallest to largest. That means rearranging the values so that a[0] is the smallest, a[1] the next smallest, and so forth. That definition yields an outline for the selection sort algorithm:

```
for (int index = 0; index < numberUsed; index++)
    Place the indexth smallest element in a[index]
```

There are many ways to realize this general approach. The details could be developed using two arrays and copying the elements from one array to the other in sorted order, but one array should be both adequate and economical. Therefore, the function sort uses only the one array containing the values to be sorted. The function sort rearranges the values in the array a by interchanging pairs of values. Let us go through a concrete example so that you can see how the algorithm works.

Consider the array shown in Display 5.7. The algorithm will place the smallest value in a[0]. The smallest value is the value in a[3], so the algorithm interchanges the values of a[0] and a[3]. The algorithm then looks for the next-smallest element. The value in a[0] is now the smallest element, and so the next-smallest element is the smallest of the remaining elements a[1], a[2], a[3], ..., a[9]. In the example in Display 5.7 the next-smallest element is in a[5], so the algorithm interchanges the values of a[1] and a[5]. This positioning of the second-smallest element is illustrated in the fourth and fifth array pictures in Display 5.7. The algorithm then positions the third-smallest element, and so forth. As the sorting proceeds, the beginning array elements are set equal to the correct sorted values. The sorted portion of the array grows by adding elements one after the other from the elements in the unsorted end of the array. Notice that the algorithm need not do anything with the value in the last indexed variable, a[9]. Once the other elements are positioned correctly, a[9] must also have the correct value. After all, the correct value for a[9] is the smallest value left to be moved, and the only value left to be moved is the value that is already in a[9].

The definition of the function sort, included in a demonstration program, is given in Display 5.8. sort uses the function indexOfSmallest to find the index of the smallest element in the unsorted end of the array, and then it does an interchange to move this next-smallest element down into the sorted part of the array.

The function swapValues, shown in Display 5.8, is used to interchange the values of indexed variables. For example, the following call will interchange the values of a[0] and a[3]:

```
swapValues(a[0], a[3]);
```

The function swapValues was explained in Chapter 4.

## Display 5.8 Sorting an Array (part 2 of 3)

```
20 int main()
21 {
22     cout << "This program sorts numbers from lowest to highest.\n";
23     int sampleArray[10], numberUsed;
24     fillArray(sampleArray, 10, numberUsed);
25     sort(sampleArray, numberUsed);
26     cout << "In sorted order the numbers are:\n";
27     for (int index = 0; index < numberUsed; index++)
28         cout << sampleArray[index] << " ";
29     cout << endl;
30     return 0;
31 }
32 
33 void fillArray(int a[], int size, int& numberUsed)
34     <The rest of the definition of fillArray is given in Display 5.5.>
35 
34 void sort(int a[], int numberUsed)
35 {
36     int indexOfNextSmallest;
37     for (int index = 0; index < numberUsed - 1; index++)
38         {//Place the correct value in a[index]:
39         indexOfNextSmallest =
40             indexOfSmallest(a, index, numberUsed);
41         swapValues(a[index], a[indexOfNextSmallest]);
42         //a[0] <= a[1] <= ... <= a[index] are the smallest of the
43         //original array elements. The rest of the
44         //elements are in the remaining positions.
45     }
46 }
47 
46 void swapValues(int& v1, int& v2)
47 {
48     int temp;
49     temp = v1;
50     v1 = v2;
51     v2 = temp;
52 }
53 
54 int indexOfSmallest(const int a[], int startIndex, int numberUsed)
55 {
56     int min = a[startIndex],
57     indexOfMin = startIndex;
```

## Display 5.8 Sorting an Array (part 3 of 3)

```
58  for (int index = startIndex + 1; index < numberUsed; index++)
59      if (a[index] < min)
60      {
61          min = a[index];
62          indexOfMin = index;
63          //min is the smallest of a[startIndex] through a[index]
64      }
65  
65  return indexOfMin;
66 }
```

## Sample Dialogue

```
This program sorts numbers from lowest to highest.
Enter up to 10 nonnegative whole numbers.
Mark the end of the list with a negative number.
80 30 50 70 60 90 20 30 40 -1
In sorted order the numbers are:
20 30 30 40 50 60 70 80 90
```

## EXAMPLE: Bubble Sort

The selection sort algorithm that we just described is not the only way to sort an array. In fact, computer scientists have devised scores of sorting algorithms! Some of these algorithms are more efficient than others, and some work only for particular types of data. Bubble sort is a simple and general sorting algorithm that is similar to selection sort.

If we use bubble sort to sort an array in ascending order, then the largest value is successively "bubbled" toward the end of the array. For example, if we start with an unsorted array consisting of the following integers:
Initial array: {3, 10, 9, 2, 5}
then after the first pass, we will have moved the largest value, 10, to the end of the array:
After first pass: {3, 9, 2, 5, 10}
The second pass will move the second largest value, 9, to the second to last index of the array:
After second pass: {3, 2, 5, 9, 10}

VideoNote
Bubble Sort
Walkthrough

The third pass will move the third largest value, 5, to the third to last index of the array (where it already is):

After third pass: {2, 3, 5, 9, 10}

The fourth pass will move the fourth largest value, 3, to the fourth to last index of the array (where it already is):

After fourth pass: {2, 3, 5, 9, 10}

At this point the algorithm is done. The remaining number at the beginning of the array doesn’t need to be examined, since it is the only number left and must be the smallest.

To design a program based on bubble sort, note that we are placing the largest item at index length-1, the second largest item at length-2, the next at length-3, etc. This corresponds to a loop that starts at index length-1 of the array and counts down to index 1 of the array. We don’t need to include index 0, since that will contain the smallest element. One way to implement the loop is with the following code, where variable i corresponds to the target index:

```
for (int i = length-1; i > 0; i--)
```

The "bubble" part of bubble sort happens inside each iteration of this loop. The bubble step consists of another loop that moves the largest number toward the end of the array. First, the largest number between index 0 and index 1 will be bubbled up to index 1. We start the bubbling procedure by comparing the number at index 0 with the number at index 1. If the number at index 0 is larger than the number at index 1, then the values are swapped, so we end up with the larger number at index 1. If the number at index 0 is less than or equal to the number at index 1, then nothing happens. We start with the following unsorted array:

Initial array: {3, 10, 9, 2, 5}

The first step of the bubbling procedure will compare 3 to 10. Since 10 > 3, nothing happens, and the end result is that the number 10 is at index 1:

After step 1: {3, 10, 9, 2, 5}

## 1. 引言

本文档旨在介绍一种新型的文档解析方法，该方法能够高效地从复杂版面中提取结构化信息。该方法结合了深度学习与传统规则，适用于多种文档类型。

- 支持标题、段落、表格等元素的识别
- 支持阅读顺序的还原
- 支持版面方向（横/竖）的自动判断

| 方法 | 准确率 | 召回率 |
|------|--------|--------|
| 传统方法 | 85% | 80% |
| 深度方法 | 95% | 92% |

> > 注意：本方法在扫描件上的效果优于纯文本文件。

![](img/c76bba8c1d927f399768ffe2ab5f5bee_249_0.png)

```
```python
import docx
print("Hello, world!")
```
```

综上所述，该方法在文档解析任务中表现优异，未来可进一步扩展到多模态场景。
