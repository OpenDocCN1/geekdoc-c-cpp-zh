Accordingly, the new one-dimensional array will be as follows.

When the user enters data, the script can iterate, as usual, through rows but to create the new one-dimensional array, iterating through columns is more convenient. The PHP script is presented next.

# file_35.5.php

```
<?php
define("ROWS", 3);
define("COLUMNS", 4);
define("ELEMENTS", ROWS * COLUMNS);

$a = array(array());
for ($i = 0; $i <= ROWS - 1; $i++) {
    for ($j = 0; $j <= COLUMNS - 1; $j++) {
        echo "Enter a value for element ", $i , ",", $j, ": ";
        $a[$i][$j] = trim(fgets(STDIN));
    }
}

$b = array();
$k = 0; //This is the index of the new array.
for ($j = 0; $j <= COLUMNS - 1; $j++) { //Iterate through columns
    for ($i = 0; $i <= ROWS - 1; $i++) {
        $b[$k] = $a[$i][$j];
        $k++;
    }
}

for ($k = 0; $k <= ELEMENTS - 1; $k++) {
    echo $b[$k], " ";
}
```

![](bbox=[0.266, 0.067, 0.914, 0.211])

![](bbox=[0.121, 0.254, 0.984, 0.306])