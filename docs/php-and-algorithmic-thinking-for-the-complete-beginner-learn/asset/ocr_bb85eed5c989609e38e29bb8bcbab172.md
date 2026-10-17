# # Chapter 42 Flowcharts with Subprograms

```
```php
$n = trim(fgets(STDIN));
while ($n > 0) {
    echo find_sum($n);
    echo "Enter a positive integer";
    $n = trim(fgets(STDIN));
}
?>```
```

Without further explanation, the corresponding flowchart is presented here.

![](bbox=[0.014, 0.249, 0.972, 0.704])

# ## Exercise 42.2-2 Designing the Flowchart

Design the flowchart that corresponds to the following code fragment.

```
```php
function get_num_of_digits($x) {
    $count = 0;
    while ($x != 0) {
        $count++;
        $x = intval($x / 10);
    }
    return $count;
}```
```