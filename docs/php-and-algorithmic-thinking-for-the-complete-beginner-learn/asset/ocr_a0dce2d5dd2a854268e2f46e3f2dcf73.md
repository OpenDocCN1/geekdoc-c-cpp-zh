# Two-Dimensional Arrays

```
```php
$i = 2;                         //Variable $i refers to Row 2.
for ($j = 0; $j <= 3; $j++) {   //This loop control structure processes all
    process $a[$i][$j];          //elements of Row 2
}
```
```

Of course, the same results can be achieved using a nested loop control structure as shown next.

```
```php
for ($i = 0; $i <= 2; $i++) {
    for ($j = 0; $j <= 3; $j++) {
        process $a[$i][$j];
    }
}
```
```

Let’s see some examples. The following code fragment lets the user enter 10 × 10 = 100 values to array $a.

```
```php
for ($i = 0; $i <= 9; $i++) {
    for ($j = 0; $j <= 9; $j++) {
        $a[$i][$j] = trim(fgets(STDIN));
    }
}
```
```

The following code fragment decreases all values of array $a by one.

```
```php
for ($i = 0; $i <= 9; $i++) {
    for ($j = 0; $j <= 9; $j++) {
        $a[$i][$j] = $a[$i][$j] - 1;
    }
}
```
```

The following code fragment displays the values of array $a.

```
```php
for ($i = 0; $i <= 9; $i++) {
    for ($j = 0; $j <= 9; $j++) {
        echo $a[$i][$j], "\t";
    }
    echo "\n";
}
```
```

# Iterating Through Columns

Iterating through columns means that column 0 is processed first, column 1 is processed next, column 2 afterwards, and so on. Next there is an example of a 3 × 4 array. The arrows show the order in which the elements are processed.