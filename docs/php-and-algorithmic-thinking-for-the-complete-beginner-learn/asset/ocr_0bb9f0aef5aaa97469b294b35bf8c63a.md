+   a. variables $i and $j as counters.  
+   b. variables $k and $l as counters.  
+   c. variables $m and $n as counters.  
+   d. any variables as counters.

8. The following code fragment

```
```php
$names = array(array("John", "Sally"),
               array("George", "Maria"));

for ($j = 0; $j <= 1; $j++) {
    for ($i = 1; $i >= 0; $i--) {
        echo $names[$i][$j];
    }
}
```
```

+   a. displays all names in descending order.  
+   b. displays some names in descending order.  
+   c. displays all names in ascending order.  
+   d. displays some names in ascending order.  
+   e. none of the above

9. If array $a contains 30 × 40 elements, the following code fragment

```
```php
for ($i = 30; $i >= 1; $i--) {
    for ($j = 40; $j >= 1; $j--) {
        $a[$i][$j] *= 3;
    }
}
```
```

+   a. triples the values of some of its elements.  
+   b. triples the values of all of its elements.  
+   c. none of the above

10. If array $a contains 30 × 40 elements, the following code fragment

```
```php
$sum = 0;

for ($i = 29; $i >= 0; $i--) {
    for ($j = 39; $j >= 0; $j--) {
        $sum += $a[$i][$j];
    }
}

$average = $sum / 120;
```
```

+   a. calculates the sum of all of its elements.  
+   b. calculates the average value of all of its elements.