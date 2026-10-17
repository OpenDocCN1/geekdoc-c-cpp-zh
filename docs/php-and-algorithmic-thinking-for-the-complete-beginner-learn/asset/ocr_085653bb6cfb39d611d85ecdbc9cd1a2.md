```
```php
<?php
define("DAYS", 31);

$names = array();
$t = array(array());
for ($i = 0; $i <= CITIES - 1; $i++) {
    echo "Enter a name for city No: ", $i + 1, ": ";
    $names[$i] = trim(fgets(STDIN));
    for ($j = 0; $j <= DAYS - 1; $j++) {
        echo "Enter a temperature for day No: ", $j + 1, ": ";
        $t[$i][$j] = trim(fgets(STDIN));
    }
}

echo "Cities in which there was a possibility of snow in January: ";
for ($i = 0; $i <= CITIES - 1; $i++) {
    $found = false;
    for ($j = 0; $j <= DAYS - 1; $j++) {
        if ($t[$i][$j] < 36) {
            $found = true;
        }
    }
    if ($found == true) {
        echo $names[$i];
    }
}
?>
```
```

# ## Exercise 37.6-4 Display from Highest to Lowest Grades by Student, and in Alphabetical Order

There are 10 students and each one of them has received his or her grades for five lessons. Write a PHP script that lets a teacher enter the name of each student and his or her grades for all lessons. The script should then calculate each student’s average grade, and display the names of the students sorted by their average grade in descending order. Moreover, if two or more students have the same average grade, their names should be displayed in alphabetical order.

# ## Solution