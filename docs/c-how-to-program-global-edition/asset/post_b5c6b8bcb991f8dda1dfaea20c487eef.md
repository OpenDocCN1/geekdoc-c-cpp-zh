
## D.3 Selection Sort

Selection sort is a simple, but inefficient, sorting algorithm. The first iteration of the algorithm selects the smallest element in the array and swaps it with the first element. The second iteration selects the second-smallest element (which is the smallest of those remaining) and swaps it with the second element. The algorithm continues until the last iteration selects the second-largest element and swaps it with the second-to-last, leaving the largest element as the last. After the ith iteration, the smallest i positions of the array will be sorted into increasing order in the first i positions of the array.

As an example, consider the array

```text
34    56    4    10    77    51    93    30    5    52
```

A program that implements selection sort first determines the smallest element (4) of this array which is contained in the third element of the array (i.e., element 2 because array subscripts start at 0). The program swaps 4 with 34, resulting in

```text
4    56    34    10    77    51    93    30    5    52
```

```cpp
84     // indicate amount of array that is sorted
85     for (unsigned int i = 0; i < pass; i++) {
86         printf("%s", "-- ");
87     }
88
89     puts(""); // add newline
90 }
```

```text
Unsorted array:
72  34  88  14  32  12  34  77  56  83
After pass  1: 12  34  88  14  32  72* 34  77  56  83
             -- 
After pass  2: 12  14  88  34* 32  72  34  77  56  83
             --  -- 
After pass  3: 12  14  32  34  88* 72  34  77  56  83
             --  --  -- 
After pass  4: 12  14  32  34* 88  72  34  77  56  83
             --  --  --  -- 
After pass  5: 12  14  32  34  34  72  88* 77  56  83
             --  --  --  --  -- 
After pass  6: 12  14  32  34  34  56  88  77  72* 83
             --  --  --  --  --  -- 
After pass  7: 12  14  32  34  34  56  72  77  88* 83
             --  --  --  --  --  --  -- 
After pass  8: 12  14  32  34  34  56  72  77* 88  83
             --  --  --  --  --  --  --  -- 
After pass  9: 12  14  32  34  34  56  72  77  83  88*
             --  --  --  --  --  --  --  --  -- 
After pass 10: 12  14  32  34  34  56  72  77  83  88*
             --  --  --  --  --  --  --  --  --  -- 
Sorted array:
12  14  32  34  34  56  72  77  83  88
```

Fig. D.1 | The selection sort algorithm. (Part 3 of 3.)

Lines 39–55 define the selectionSort function. Line 43 declares the variable smallest, which stores the index of the smallest element in the remaining array. Lines 42–54 loop length - 1 times. Line 43 assigns to smallest the index i—representing the first index of the unsorted portion of the array. Lines 46–50 loop over the remaining elements in the array. For each of these elements, line 47 compares the current element’s value to the value of the element at index smallest. If the current element is smaller, line 48 assigns the current element’s index to smallest. When this loop finishes, smallest contains the index of the smallest element in the remaining array. Line 52 calls function swap (lines 58–63) to place the smallest remaining element in the next spot in the array.

The output of this program uses dashes to indicate the portion of the array that is guaranteed to be sorted after each pass. An asterisk is placed next to the position of the element that was swapped with the smallest element on that pass. On each pass, the element to the left of the asterisk and the element above the rightmost set of dashes were the two values that were swapped.

### Efficiency of Selection Sort

The selection sort algorithm runs in O(n^2) time. The selectionSort method in Fig. D.1—which implements the algorithm—contains two for loops. The outer for loop (lines 42–54) iterates over the first n − 1 elements in the array, swapping the smallest remaining item into its sorted position. The inner for loop (lines 46–50) iterates over each item in the remaining array, searching for the smallest element. This loop executes n − 1 times during the first iteration of the outer loop, n − 2 times during the second iteration, then n − 3, . . . , 3, 2, 1. This inner loop iterates a total of n(n − 1) / 2 or (n^2 − n)/2. In Big O notation, smaller terms drop out and constants are ignored, leaving a Big O of O(n^2).

## D.4 Insertion Sort

Insertion sort is another simple, but inefficient, sorting algorithm. The first iteration of this algorithm takes the second element in the array and, if it's less than the first element, swaps it with the first element. The second iteration looks at the third element and inserts it into the correct position with respect to the first two elements, so all three elements are in order. At the ith iteration of this algorithm, the first i elements in the original array will be sorted.

Consider as an example the following array [Note: This array is identical to the one used in the discussions of selection sort and merge sort.]

```text
    34   56   4   10   77   51   93   30   5   52
```

A program that implements the insertion sort algorithm will first look at the first two elements of the array, 34 and 56. These two elements are already in order, so the program continues (if they were out of order, the program would swap them).

In the next iteration, the program looks at the third value, 4. This value is less than 56, so the program stores 4 in a temporary variable and moves 56 one element to the right. The program then checks and determines that 4 is less than 34, so it moves 34 one element to the right. The program has now reached the beginning of the array, so it places 4 in element 0. The array now is

```text
    4   34   56   10   77   51   93   30   5   52
```

In the next iteration, the program stores the value 10 in a temporary variable. Then the program compares 10 to 56 and moves 56 one element to the right because it's larger than 10. The program then compares 10 to 34, moving 34 right one element. When the program compares 10 to 4, it observes that 10 is larger than 4 and places 10 in element 1. The array now is

```text
    4   10   34   56   77   51   93   30   5   52
```

Using this algorithm, after the ith iteration, the first i + 1 elements of the original array are sorted with respect to one another. They may not be in their final locations, however, because smaller values may be located later in the array.

Figure D.2 implements the insertion sort algorithm. Lines 38–55 define the insertionSort function. The variable insert (line 43) holds the element you're going to insert while you move the other elements. Lines 41–54 iterate over the items in the array from index 1 through the end. In each iteration, line 42 initializes the variable moveItem, which keeps track of where to insert the element, and line 43 stores in insert the value that will be inserted into the sorted portion of the array. Lines 46–50 loop to locate the position where the element should be inserted. The loop terminates either when the program reaches the front of the array or when it reaches an element that is less than the value to be
