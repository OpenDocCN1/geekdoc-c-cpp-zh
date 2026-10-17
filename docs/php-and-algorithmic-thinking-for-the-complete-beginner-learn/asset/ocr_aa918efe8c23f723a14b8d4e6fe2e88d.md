# # Exercise 31.6-2 Wheat on a Chessboard

On a chessboard you must place grains of wheat on each square, such that one grain is placed on the first square, two on the second, four on the third, and so on (doubling the number of grains on each subsequent square). How many grains of wheat will be on the chessboard in the end?

# ## Solution

Assume a chessboard of only 2 × 2 = 4 squares and a variable $grains assigned the initial value 1 (this is the number of grains of the 1st square). A counted loop structure that iterates three times can double the value of variable $grains in each iteration, as shown in the next code fragment.

```
```php
$grains = 1;
for ($i = 2; $i <= 4; $i++) {
    $grains = 2 * $grains;
}
```
```

The value of variable $grains at the end of each iteration is shown in the next table.

| Iteration | Value of i | Value of grains |
|-----------|------------|-----------------|
| 1st       | 2          | 2 × 1 = 2       |
| 2nd       | 3          | 2 × 2 = 4       |
| 3rd       | 4          | 2 × 4 = 8       |

At the end of the 3rd iteration, variable $grains contains the value 8. This value, however, is not the total number of grains on the chessboard but only the number of grains on the 4th square. If you need to find the total number of grains on the chessboard you can sum up the grains on all squares, that is, 1 + 2 + 4 + 8 = 15.

In the real world a real chessboard contains 8 × 8 = 64 squares, thus you need to iterate for 64 times. The PHP script is as follows.

```
```php
<?php
$grains = 1;
$sum = 1;
for ($i = 2; $i <= 64; $i++) {
    $grains = 2 * $grains;
    $sum = $sum + $grains;
}
echo $sum;
?>
```
```

In case you are wondering how big this number is, here is your answer: On the chessboard there will be 18,446,744,073,709,551,615 grains of wheat!