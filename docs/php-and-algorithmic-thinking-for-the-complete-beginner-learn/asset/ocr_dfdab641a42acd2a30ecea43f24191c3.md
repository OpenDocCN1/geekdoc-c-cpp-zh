```
if ($count == COLUMNS) {
    echo $needle, " found in every column!";
}
?>
```

**Notice:** If you need a message to be displayed when a given value exists at least once in each **row**, the PHP script can do the same as previously shown; however, instead of iterating through columns, it has to iterate through rows.

# Exercise 37.5-8 The Binary Search Algorithm – Searching in a Sorted One-Dimensional Array

Write a code fragment that searches a sorted one-dimensional array for a given value. Use the binary search algorithm.

# Solution

The binary search algorithm is considered very fast and can be used with large scale data. Its main disadvantage, though, is that the data need to be sorted.

The main idea of the binary search algorithm is to check the value of the element in the middle (approximately). If it is not the “needle in the haystack” that you are looking for, and what you are looking for is actually smaller than the value of the middle element, it means that the “needle” must be in the first half of the array. On the other hand, if what you are looking for is larger than the value of the middle element, it means that the “needle” must be in the last half of the array.

The binary search algorithm continues by checking the value of the middle element in the remaining half part of the array. If it’s still not the “needle,” the search narrows to the half of the remaining part of the array that the “needle” could be in. This “splitting” process continues until the “needle” is found or the remaining part of the array consists of only one element. If that element is not the “needle,” then the given value is not in the array.

Confused? Let’s try to analyze a binary search algorithm through an example. The following array contains numeric values in ascending order. Assume that the “needle” that you are looking for is the value 44.

|   | 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   | 10  | 11  | 12  | 13  |
|---|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| A = | 12  | 15  | 19  | 24  | 28  | 31  | 39  | 41  | 44  | 53  | 57  | 59  | 62  | 64  |

Three variables are used. Initially, variable `$start` contains the value 0 (this is the index of the first element), variable `$end` contains the value 12 (this is the index of the last element) and variable `$middle` contains the value 6 (this is approximately the index of the middle element).