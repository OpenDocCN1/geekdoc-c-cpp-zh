```
$new = array();
for ($i = 0; $i <= ELEMENTS_OF_NEW - 1; $i++) {
    $new[$i] = ($a[$i] + $a[$i + 1] + $a[$i + 2]) / 3;
}

for ($i = 0; $i <= ELEMENTS_OF_NEW - 1; $i++) {
    echo $new[$i], "\t";
}
?>
```

# Exercise 37.1-2 Creating an Array with the Greatest Values

Design a flowchart and write the corresponding PHP script that lets the user enter numerical values into arrays $a and $b of 20 elements each. Then the algorithm, and consequently the script, should create a new array $new of 20 elements. The new array should contain in each position the greatest value of arrays $a and $b of the corresponding position.

# Solution

Nothing new here! You need four counted loop structures: two counted loop structures to read the values for arrays $a and $b, one for creating the array $new, and one to display array $new on the screen. The flowchart is presented next.

![](bbox=[0.188, 0.559, 0.664, 0.875])