```
```php
$max = $a[0][$j];
for ($i = 1; $i <= ROWS - 1; $i++) {
    if ($a[$i][$j] < $min) {
        $min = $a[$i][$j];
    }
    if ($a[$i][$j] > $max) {
        $max = $a[$i][$j];
    }
}
echo $min, $max;
}
?>
```
```

# 37.4　Sorting Arrays

Sorting algorithms are an important topic in computer science. A sorting algorithm is an algorithm that puts elements of an array in a certain order. There are many sorting algorithms and each one of them has particular strengths and weaknesses.

Most sorting algorithms work by comparing the elements of the array. They are usually evaluated by their efficiency and their memory requirements.

There are many sorting algorithms. Some of them are:

+   - the bubble sort algorithm
+   - the modified bubble sort algorithm
+   - the selection sort algorithm
+   - the insertion sort algorithm
+   - the heap sort algorithm
+   - the merge sort algorithm
+   - the quicksort algorithm

As regards their efficiency, the bubble sort algorithm is considered the least efficient, while each succeeding algorithm in the list performs better than the preceding one. The quicksort algorithm is considered one of the best and fastest sorting algorithms, especially for large scale data operations.

Sorting algorithms can be used for more than just displaying data in ascending or descending order. For example, if an exercise requires you to display the three biggest numbers of an array, the PHP script can sort the array in descending order and then display only the first three elements, that is, those at index positions 0, 1, and 2.

Sorting algorithms can also help you find the minimum and the maximum values from a set of given values. If an array is sorted in ascending order, the minimum value exists at the first index position and the maximum value exists at the last index position. Of course, it is very inefficient to sort an array so as to find minimum and maximum values; you have already learned a more efficient method. But if for some