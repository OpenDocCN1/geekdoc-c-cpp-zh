```
for ($i = 0; $i <= LESSONS - 1; $i++) {
    echo "Enter grade No. ", $i + 1, " for ", $names[$j], ": ";
    $grades[$i][$j] = trim(fgets(STDIN));
}
}
//Create array $count
$count = array();
for ($j = 0; $j <= STUDENTS - 1; $j++) {
    $count[$j] = 0;
    for ($i = 0; $i <= LESSONS - 1; $i++) {
        if ($grades[$i][$j] > 89) {
            $count[$j]++;
        }
    }
}
//Displays the names of the students who have
//more than one grades greater than 89
for ($j = 0; $j <= STUDENTS - 1; $j++) {
    if ($count[$j] > 1) {
        echo $names[$j], "\n";
    }
}
?>
```

# ## 35.5 Creating a One-Dimensional Array from a Two-Dimensional Array

To more easily understand how to create a one-dimensional array from a two-dimensional array, let’s use an example.

Write a script that creates a one-dimensional array of 12 elements from a two-dimensional array of 3 × 4 as follows: The elements of the first column of the two-dimensional array should be placed in the first three positions in the one-dimensional array, the elements of the second column should be placed in the next three positions, and so on.

An example of a 3 × 4 array is as follows.