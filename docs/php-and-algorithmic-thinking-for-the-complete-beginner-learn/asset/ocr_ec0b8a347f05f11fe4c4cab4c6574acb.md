```
$max = $a1;
if ($a2 > $max) {
    $max = $a2;
}
if ($a3 > $max) {
    $max = $a3;
}
...
if ($a20 > $max) {
    $max = $a20;
}
}
```

```
$count = 0;
if ($a1 == $max) {
    $count++;
}
if ($a2 == $max) {
    $count++;
}
if ($a3 == $max) {
    $count++;
}
...
if ($a20 == $max) {
    $count++;
}
}
```

echo $count;
?>

This script appears to work fine, but what if 2000 instead of 20 grades have to be entered? Think about it—do you have the patience to write an analogous PHP script for 2000 grades? Of course not! Fortunately for you, there are arrays!

# ## 32.2 What is an Array?

An array is a special type of variable that can hold multiple values at the same time under one common name. An array can be thought of as a collection of positions, each containing one value, organized in rows, columns, or a matrix. Some examples of arrays are as follows.

![](bbox=[0.414, 0.072, 0.797, 0.131])

![](bbox=[0.414, 0.343, 0.969, 0.402])