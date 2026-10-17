```
$index_of_min = $n;
}
}
//Swap values
$temp = $a[$m];
$a[$m] = $a[$index_of_min];
$a[$index_of_min] = $temp;
}
```

**Notice:** If you wish to sort an array in descending order, all you need to do is search for maximum instead of minimum values.

**Remember!** As in a bubble sort algorithm, in order to sort alphanumeric data, you can do one simple thing: leave the algorithm as is!

# ## Exercise 37.4-9 Sorting One-Dimensional Arrays While Preserving the Relationship with a Second Array

Write a PHP script that prompts the user to enter the electric meter reading recorded at the end of each month for a period of one year. It then displays each reading (in descending order) along with the name of the corresponding month. Use the selection sort algorithm.

# ## Solution

In this exercise you need the following two one-dimensional arrays.

![](bbox=[0.201, 0.604, 0.799, 0.759])

The approach is the same as in the bubble sort algorithm. While the selection sort algorithm sorts the elements of array $kwh, the relationship with the elements of array $months must also be preserved. This means that every time two elements of array $kwh swap contents, the corresponding elements of array $months must swap their contents as well. The PHP script is as follows.

```
file_37.4-9.php
```

```
<?php
define("ELEMENTS", 12);
$months = array("January", "February", "March", "April",
```