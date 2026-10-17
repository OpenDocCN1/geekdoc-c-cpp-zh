# More Exercises with Arrays

Using the “from inner to outer” method, the next code fragment sorts only the first row (row index 0) of the two-dimensional array `$elapsed_times` in descending order using the insertion sort algorithm. Assume variable `$i` contains the value 0.

```
```php
for ($m = 1; $m <= LAPS - 1; $m++) {
    $element = $elapsed_times[$i][$m];
    $n = $m;
    while($n > 0 && $elapsed_times[$i][$n - 1] < $element) {
        $elapsed_times[$i][$n] = $elapsed_times[$i][$n - 1];
        $n--;
    }
    $elapsed_times[$i][$n] = $element;
}
```
```

Now, in order to sort all rows, you need to nest this code fragment in a counted loop structure that iterates for all of them, as follows.

```
```php
for ($i = 0; $i <= CARS - 1; $i++) {
    for ($m = 1; $m <= LAPS - 1; $m++) {
        $element = $elapsed_times[$i][$m];
        $n = $m;
        while($n > 0 && $elapsed_times[$i][$n - 1] < $element) {
            $elapsed_times[$i][$n] = $elapsed_times[$i][$n - 1];
            $n--;
        }
        $elapsed_times[$i][$n] = $element;
    }
}
```
```

And now, let’s focus on the given exercise. The final PHP script is as follows.

```
```php
// file_37.4-11.php
<?php
define("CARS", 10);
define("LAPS", 20);

// Read names and elapsed times all together
$names = array();
$elapsed_times = array(array());
for ($i = 0; $i <= CARS - 1; $i++) {
    echo "Enter name for driver No. ", $i + 1, ": ";
    $names[$i] = trim(fgets(STDIN));
    for ($j = 0; $j <= LAPS - 1; $j++) {
        echo "Enter elapsed time for lap No. ", $j + 1, ": ";
```
```