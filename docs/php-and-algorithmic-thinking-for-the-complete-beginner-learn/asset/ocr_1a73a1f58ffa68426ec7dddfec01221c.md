//Display which number appears in the array most often.
echo $max_i;

But now that you are reaching the end of the book, of course, you can do something more creative. Instead of assigning each result of the `search_and_count()` function to individual variables `$n1`, `$n2`, `$n3`, `$n4`, `$n5`, and `$n6`, you can assign those results to the positions 0, 1, 2, 3, 4, and 5 of an array named `$n`, as shown here.

$n = array();
for ($i = 0; $i <= 5; $i++) {
$n[$i] = search_and_count($i + 1, $a);
}

Next, of course, you can find the maximum of the array `$n` as usual. The complete solution is shown here.

# file_43.1-5.php

```
<?php
define("ELEMENTS", 100);
function dice() {
return rand(1, 6);
}
function search_and_count($x, $a) {
$count = 0;
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
if ($a[$i] == $x) {
$count++;
}
}
return $count;
}
//Create array $a of random integers between 1 and 6
$a = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
$a[] = dice();
}
//Create array $n and
```