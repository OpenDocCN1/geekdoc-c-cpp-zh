# # Exercise 37.3-7 Finding the Minimum and the Maximum Value of Each Row

Write a PHP script that lets the user enter values in a 20 × 30 array and then finds and displays the minimum and the maximum values of each row.

# ## Solution

There are two approaches, actually. The first approach creates two auxiliary one-dimensional arrays, $min and $max, and then displays them. Arrays $min and $max will contain, in each position, the minimum and the maximum values of each row respectively. On the other hand, the second approach finds and directly displays the minimum and maximum values of each row. Let’s study both approaches.

# ### First Approach – Creating auxiliary arrays

To better understand this approach, let’s use the “from inner to outer” method. When the following code fragment completes its iterations, the auxiliary one-dimensional arrays $min and $max contain at position 0 the minimum and the maximum values of the first row (row index 0) of array $a respectively. Assume variable $i contains value 0.

```
```php
$min[$i] = $a[$i][0];
$max[$i] = $a[$i][0];
for ($j = 1; $j <= COLUMNS - 1; $j++) {
    if ($a[$i][$j] < $min[$i]) {
        $min[$i] = $a[$i][$j];
    }
    if ($a[$i][$j] > $max[$i]) {
        $max[$i] = $a[$i][$j];
    }
}
```
```

> > Notice: Please note that the initial value of variable $j is 1. It wouldn’t be wrong to start iterating from column index 0 instead of 1, though the script would perform one useless iteration.

Now that everything has been clarified, in order to process the whole array $a, you can just nest this code fragment into a counted loop structure which iterates for all rows as shown next.

```
```php
for ($i = 0; $i <= ROWS - 1; $i++) {
    $min[$i] = $a[$i][0];
    $max[$i] = $a[$i][0];
    for ($j = 1; $j <= COLUMNS - 1; $j++) {
        if ($a[$i][$j] < $min[$i]) {
            $min[$i] = $a[$i][$j];
        }
    }
}
```
```