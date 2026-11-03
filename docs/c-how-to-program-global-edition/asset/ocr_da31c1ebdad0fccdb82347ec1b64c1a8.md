```
~~~cpp
84     // indicate amount of array that is sorted
85     for (unsigned int i = 0; i < pass; i++) {
86         printf("%s", "-- ");
87     }
88
89     puts(""); // add newline
90 }
~~~
```

```
~~~text
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
~~~
```

Fig. D.1 | The selection sort algorithm. (Part 3 of 3.)

Lines 39–55 define the selectionSort function. Line 43 declares the variable smallest, which stores the index of the smallest element in the remaining array. Lines 42–54 loop length - 1 times. Line 43 assigns to smallest the index i—representing the first index of the unsorted portion of the array. Lines 46–50 loop over the remaining elements in the array. For each of these elements, line 47 compares the current element’s value to the value of the element at index smallest. If the current element is smaller, line 48 assigns the current element’s index to smallest. When this loop finishes, smallest contains the index of the smallest element in the remaining array. Line 52 calls function swap (lines 58–63) to place the smallest remaining element in the next spot in the array.

The output of this program uses dashes to indicate the portion of the array that is guaranteed to be sorted after each pass. An asterisk is placed next to the position of the element that was swapped with the smallest element on that pass. On each pass, the element to the left of the asterisk and the element above the rightmost set of dashes were the two values that were swapped.

# Efficiency of Selection Sort

The selection sort algorithm runs in O(n^2) time. The selectionSort method in Fig. D.1—which implements the algorithm—contains two for loops. The outer for loop (lines 42–