```
iii)
```php
for ($i = 0; $i <= 2; $i++) {
    for ($j = 2; $j >= 0; $j--)
        echo $a[$i][$j], " ";
}
```

```

```
iv)
```php
for ($i = 2; $i >= 0; $i--)
    for ($j = 2; $j >= 0; $j--)
        echo $a[$i][$j], " ";
```

```

```
v)
```php
for ($j = 0; $j <= 2; $j++) {
    for ($i = 0; $i <= 2; $i++)
        echo $a[$i][$j], " ";
}
```

```

```
vi)
```php
for ($j = 0; $j <= 2; $j++) {
    for ($i = 2; $i >= 0; $i--)
        echo $a[$i][$j], " ";
}
```

```

```
vii)
```php
for ($j = 2; $j >= 0; $j--) {
    for ($i = 0; $i <= 2; $i++)
        echo $a[$i][$j], " ";
}
```

```

```
viii)
```php
for ($j = 2; $j >= 0; $j--)
    for ($i = 2; $i >= 0; $i--)
        echo $a[$i][$j], " ";
```

```

+   9. Write a PHP script that lets the user enter integer values in a 10 × 15 array and then displays the indexes of the positions that contain odd numbers.
+   
+   10. Write a PHP script that lets the user enter numeric values in a 10 × 6 array and then displays the elements of the columns with even-numbered indexes (that is, column indexes 0, 2, and 4).
+   
+   11. Write a PHP script that lets the user enter numeric values in a 12 × 8 array and then calculates and displays the sum of the elements that have even column indexes and odd row indexes.
+   
+   12. Write a PHP script that lets the user enter numeric values in an 8 × 8 square array and then calculates the average value of the elements of its main diagonal and the average value of the elements of its antidiagonal. Try to calculate both average values within the same loop control structure.
+   
+   13. Write a PHP script that creates and displays the following array.

$a =

|   | 0 | 1 | 2 | 3 | 4 |
|---|---:|---:|---:|---:|---:|
| 0 | 11 | 11 | 11 | 11 | 5 |
| 1 | 11 | 11 | 11 | 5 | 88 |
| 2 | 11 | 11 | 5 | 88 | 88 |
| 3 | 11 | 5 | 88 | 88 | 88 |
| 4 | 5 | 88 | 88 | 88 | 88 |