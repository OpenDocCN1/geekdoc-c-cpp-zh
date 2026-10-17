
# Second Approach – Finding and directly displaying minimum and maximum values

Without further clarification, and using the second approach of the previous exercise as a guide, the corresponding solution is as follows.

```php
<?php
define("ROWS", 30);
define("COLUMNS", 20);

$a = array(array());
for ($i = 0; $i <= ROWS - 1; $i++) {
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        $a[$i][$j] = trim(fgets(STDIN));
    }
}

for ($j = 0; $j <= COLUMNS - 1; $j++) {
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

# 37.4 Sorting Arrays

Sorting algorithms are an important topic in computer science. A sorting algorithm is an algorithm that puts elements of an array in a certain order. There are many sorting algorithms and each one of them has particular strengths and weaknesses.

Most sorting algorithms work by comparing the elements of the array. They are usually evaluated by their efficiency and their memory requirements.

There are many sorting algorithms. Some of them are:

- the bubble sort algorithm
- the modified bubble sort algorithm
- the selection sort algorithm
- the insertion sort algorithm
- the heap sort algorithm
- the merge sort algorithm
- the quicksort algorithm

As regards their efficiency, the bubble sort algorithm is considered the least efficient, while each succeeding algorithm in the list performs better than the preceding one. The quicksort algorithm is considered one of the best and fastest sorting algorithms, especially for large scale data operations.

Sorting algorithms can be used for more than just displaying data in ascending or descending order. For example, if an exercise requires you to display the three biggest numbers of an array, the PHP script can sort the array in descending order and then display only the first three elements, that is, those at index positions 0, 1, and 2.

Sorting algorithms can also help you find the minimum and the maximum values from a set of given values. If an array is sorted in ascending order, the minimum value exists at the first index position and the maximum value exists at the last index position. Of course, it is very inefficient to sort an array so as to find minimum and maximum values; you have already learned a more efficient method. But if for some reason an exercise requires that an array be sorted and you need the minimum or the maximum value, you know where you can find them!

# Exercise 37.4-1 The Bubble Sort Algorithm – Sorting One-Dimensional Arrays with Numeric Values

Write a PHP script that lets the user enter 20 numerical values into an array and then sorts them in ascending order using the bubble sort algorithm.

# Solution

The bubble sort algorithm is probably one of the most inefficient sorting algorithms but it is widely used for teaching purposes. The main idea (when asked to sort an array in ascending order) is to repeatedly move the smallest elements of the array to the positions of lowest index. This works as follows: the algorithm iterates through the elements of the array, compares each pair of adjacent elements, and then swaps their contents (if they are in the wrong order). This process is repeated many times until the array is sorted.

For example, let’s try to sort the following array in ascending order.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_702_0.png)

The lowest value is the value 5. According to the bubble sort algorithm, this value should gradually “bubble” or “rise” to position 0, like bubbles rising in a glass of cola. When the value 5 has been moved into position 0, the next smallest value is the value 8. Now, the value 8 should “bubble” to position 1. Next is the value 12, which should “bubble” to position 2, and so on. This process repeats until all elements are placed in proper position.

But how can this “bubbling” be done using an algorithm? Let’s see the whole process in more detail. For the previous array A of six elements, five passes must be performed.

# First Pass

# 1st Compare

Initially, elements at index positions 4 and 5 are compared. Since the value 12 is less than the value 49, these two elements swap their content.

# 2nd Compare

Elements at index positions 3 and 4 are compared. Since the value 12 is **not** less than the value 5, **no** swapping is done.

# 3rd Compare

Elements at index positions 2 and 3 are compared. Since the value 5 is less than the value 8, these two elements swap their content.

# 4th Compare

Elements at index positions 1 and 2 are compared. Since the value 5 is less than the value 25, these two elements swap their content.

# 5th Compare

Elements at index positions 0 and 1 are compared. Since the value 5 is less than the value 17, these two elements swap their content.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_703_0.png)

The first pass has been completed but, as you can see, the array has not been sorted yet. The only value that has actually been placed in proper position is the value 5. However, since more passes will follow, there is no need for the value 5 to take part in the subsequent compares. In the pass that follows, one less compare will be performed—that is, four compares.

# Second Pass

# 1st Compare

Elements at index positions 4 and 5 are compared. Since the value 49 is **not** less than the value 12, **no** swapping is done.

# 2nd Compare

Elements at index positions 3 and 4 are compared. Since the value 12 is **not** less than the value 8, **no** swapping is done.

# 3rd Compare

Elements at index positions 2 and 3 are compared. Since the value 8 is less than the value 25, these two elements swap their content.

# 4th Compare

Elements at index positions 1 and 2 are compared. Since the value 8 is less than the value 17, these two elements swap their content.

# Chapter 37 More Exercises with Arrays

![](img/4d9a992abc5da7946ac44f9e6bf1d032_704_0.png)

The second pass has been completed and the value of 8 has been placed in proper position. However, since more passes will follow, there is no need for the value 8 (nor 5, of course) to take part in the subsequent compares. In the pass that follows, one less compare will be performed—that is, three compares.

# Third Pass

# 1st Compare

Elements at index positions 4 and 5 are compared. Since the value 49 is **not** less than the value 12, **no** swapping is done.

# 2nd Compare

Elements at index positions 3 and 4 are compared. Since the value 12 is less than the value 25, these two elements swap their content.

# 3rd Compare

Elements at index positions 2 and 3 are compared. Since the value 12 is less than the value 17, these two elements swap their content.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_704_1.png)

The third pass has been completed and the value of 12 has been placed in proper position. As previously, since more passes will follow there is no need for the value 12 (nor the values 5 and 8, of course) to take part in the subsequent compares. In the pass that follows, one compare less will be performed—that is, two compares.

# Fourth Pass

# 1st Compare

Elements at index positions 4 and 5 are compared. Since the value 49 is **not** less than the value 25, **no** swapping is done.

# 2nd Compare

Elements at index positions 3 and 4 are compared. Since the value 25 is **not** less than the value 17, **no** swapping is done.

The fourth pass has been completed and the value 17 has been placed in proper position. As previously, since one last pass will follow, there is no need for the value 17 (nor the values 5, 8, and 12, of course) to take part in the subsequent compares. In the last pass that follows, one compare less will be performed—that is one compare.

# Fifth pass

# 1st Compare

Elements at index positions 4 and 5 are compared. Since the value 49 is **not** less than the value 12, **no** swapping is done.

The fifth pass has been completed and the final two values (25 and 49) have been placed in proper position. The bubble sort algorithm has finished and the array is sorted in ascending order!

Now you need a PHP script that can do the whole previous process. Let’s use the “from inner to outer” method. The code fragment that performs the first pass is

![](img/4d9a992abc5da7946ac44f9e6bf1d032_705_0.png)

![](img/4d9a992abc5da7946ac44f9e6bf1d032_705_1.png)
