```
}
$average[$j] /= STUDENTS;
}

//Display all average values than are greater than 89
for ($j = 0; $j <= LESSONS - 1; $j++) {
    if ($average[$j] > 89) {
        echo $average[$j], "\n";
    }
}
?>
```

# ## Second Approach – Just find it and display it!

This approach uses no auxiliary array; it just calculates and directly displays all average values that are greater than 89. The PHP script is as follows.

```
file_35.3-1b.php
<?php
define("STUDENTS", 10);
define("LESSONS", 5);

$grades = array(array());
for ($i = 0; $i <= STUDENTS - 1; $i++) {
    echo "For student No. ", $i + 1, "...\n";
    for ($j = 0; $j <= LESSONS - 1; $j++) {
        echo "enter grade for lesson No. ", $j + 1 , ": ";
        $grades[$i][$j] = trim(fgets(STDIN));
    }
}

//Calculate the average value of each column individually
//and directly display those who are greater than 89
for ($j = 0; $j <= LESSONS - 1; $j++) {
    $average = 0;
    for ($i = 0; $i <= STUDENTS - 1; $i++) {
        $average += $grades[$i][$j];
    }
    $average /= STUDENTS;
    if ($average > 89) {
        echo $average, "\n";
    }
}
```