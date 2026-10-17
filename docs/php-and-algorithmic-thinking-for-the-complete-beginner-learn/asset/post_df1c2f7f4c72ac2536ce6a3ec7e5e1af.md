

# Exercise 37.4-4  *Sorting Last and First Names*

Write a PHP script that prompts the user to enter the last and first names of 100 people and then displays them with the last names sorted in alphabetical order. Moreover, if two or more people have the same last name, their first names should be displayed in alphabetical order as well.

# Solution

In this exercise, you need the following two arrays.

# Chapter 37 More Exercises with Arrays

Of course, you already know how to sort the array `$last_names` and at the same time preserve the relationship with the elements of the array `$first_names`. But, what you actually don’t know here is how to handle the case when two last names are equal. According to the wording of the exercise, the corresponding first names should be also sorted alphabetically.

For your convenience, the basic version of the bubble sort algorithm is presented once again. Please note that this algorithm preserves the relationship between the elements of arrays `$last_names` and `$first_names`.

```
for ($m = 1; $m <= PEOPLE - 1; $m++) {
for ($n = PEOPLE - 1; $n >= $m; $n--) {
if ($last_names[$n] < $last_names[$n - 1]) {
$temp = $last_names[$n];
$last_names[$n] = $last_names[$n - 1];
$last_names[$n - 1] = $temp;

$temp = $first_names[$n];
$first_names[$n] = $first_names[$n - 1];
$first_names[$n - 1] = $temp;
}
}
}
```

To solve this exercise, however, this bubble sort algorithm must be adapted accordingly. According to this basic version of the bubble sort algorithm, when the last name at position `$n` is “less” than the last name at position `$n - 1`, the algorithm swaps the corresponding contents as usual. However, when the last name at position `$n` is equal to the last name at position `$n - 1`, the algorithm then must check if the corresponding first names are in the proper order. If not, they should swap their contents. The adapted bubble sort algorithm is shown in the next code fragment.

```
for ($m = 1; $m <= PEOPLE - 1; $m++) {
for ($n = PEOPLE - 1; $n >= $m; $n--) {
if ($last_names[$n] < $last_names[$n - 1]) {
$temp = $last_names[$n];
$last_names[$n] = $last_names[$n - 1];
$last_names[$n - 1] = $temp;
}
```

![](img/4d9a992abc5da7946ac44f9e6bf1d032_710_0.png)

# Chapter 37  
More Exercises with Arrays

```
$temp = $first_names[$n];
$first_names[$n] = $first_names[$n - 1];
$first_names[$n - 1] = $temp;
}
elseif ($last_names[$n] == $last_names[$n - 1]) {
    if ($first_names[$n] < $first_names[$n - 1]) {
        $temp = $first_names[$n];
        $first_names[$n] = $first_names[$n - 1];
        $first_names[$n - 1] = $temp;
    }
}
}
}
```

The final PHP script is presented next.

```
<?php
define("PEOPLE", 100);

//Read arrays $first_names and $last_names
$first_names = array();
$last_names = array();
for ($i = 0; $i <= PEOPLE - 1; $i++) {
    echo "Enter first name for person No. ", $i + 1, ": ";
    $first_names[$i] = trim(fgets(STDIN));
    echo "Enter last name for person No. ", $i + 1, ": ";
    $last_names[$i] = trim(fgets(STDIN));
}

for ($m = 1; $m <= PEOPLE - 1; $m++) {
    for ($n = PEOPLE - 1; $n >= $m; $n--) {
        if ($last_names[$n] < $last_names[$n - 1]) {
            $temp = $last_names[$n];
            $last_names[$n] = $last_names[$n - 1];
            $last_names[$n - 1] = $temp;

            $temp = $first_names[$n];
            $first_names[$n] = $first_names[$n - 1];
            $first_names[$n - 1] = $temp;
```

```
$temp = $a[$n][$j];
$a[$n][$j] = $a[$n - 1][$j];
$a[$n - 1][$j] = $temp;
}
}
}
```

Now, in order to sort all columns, you can nest this code fragment in a counted loop structure that iterates for all of them, as follows.

```
for ($j = 0; $j <= COLUMNS - 1; $j++) {
    for ($m = 1; $m <= ROWS - 1; $m++) {
        for ($n = ROWS - 1; $n >= $m; $n--) {
            if ($a[$n][$j] < $a[$n - 1][$j]) {
                $temp = $a[$n][$j];
                $a[$n][$j] = $a[$n - 1][$j];
                $a[$n - 1][$j] = $temp;
            }
        }
    }
}
```

That wasn’t so difficult, was it?

# Exercise 37.4-6  The Modified Bubble Sort Algorithm – Sorting One-Dimensional Arrays

Write a PHP script that lets the user enter the weights of 30 people and then displays the three heaviest weights and the three lightest weights. Use the **modified bubble sort** algorithm.

# Solution

To solve this exercise, the PHP script can sort the given data in ascending order and then display the elements at index positions 27, 28, and 29 (for the three heaviest weights) and the elements at index positions 0, 1 and 2 (for the three lightest weights).

But how does the modified version of the bubble sort algorithm actually work? Suppose you have the following array containing the weights of six people.

| 0 | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| 165 | 170 | 180 | 190 | 182 | 200 |

If you look closer, you can confirm for yourself that the only elements that are not in proper position are those at index positions 3 and 4. If you swap their values, the array $W$ immediately becomes sorted! However, the bubble sort algorithm doesn’t operate this way. Unfortunately, for this given array of six elements, it will perform five passes either way, with a total of $\frac{N(N-1)}{2}=15$ compares, where $N$ is the total number of array elements. For bigger arrays, the total number of compares that the bubble sort algorithm performs increases exponentially!

Of course the modified bubble sort algorithm can overcome this situation as follows: if a complete pass is performed and no swaps have been made, then the array is sorted and there is no need for further passes. To accomplish this, the PHP script can use a flag variable that indicates if any swaps were made. At the beginning of a pass, a value of `false` can be assigned to the flag variable; when a swap is made, a value of `true` is assigned. If, at the end of the pass, the flag is still false, this indicates that no swaps have been made, thus iterations should stop. The modified bubble sort is shown next in two versions.

The next approach uses the `break` statement and a flag variable (`$swaps`).

```
for ($m = 1; $m <= ELEMENTS - 1; $m++) {
    $swaps = false;

    for ($n = ELEMENTS - 1; $n >= $m; $n--) {
        if ($W[$n] < $W[$n - 1]) {
            $temp = $W[$n];
            $W[$n] = $W[$n - 1];
            $W[$n - 1] = $temp;

            $swaps = true;
        }
    }

    if ($swaps == false) break;
}
```

The next approach, on the other hand, uses a pre-test loop structure and a flag variable.

```
$m = 1;
$swaps = true;

while ($m <= ELEMENTS - 1 && $swaps == true) {
    $swaps = false;

    for ($n = ELEMENTS - 1; $n >= $m; $n--) {
        if ($W[$n] < $W[$n - 1]) {
            $temp = $W[$n];
            $W[$n] = $W[$n - 1];
            $W[$n - 1] = $temp;

            $swaps = true;
```

So, let’s now focus on the given exercise. The final PHP script is shown next. It uses the approach with the break statement, but you can easily rewrite it and make use of the second approach.

```
<?php
define("ELEMENTS", 20);

$w = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    $w[$i] = trim(fgets(STDIN));
}

for ($m = 1; $m <= ELEMENTS - 1; $m++) {
    $swaps = false;
    for ($n = ELEMENTS - 1; $n >= $m; $n--) {
        if ($w[$n] < $w[$n - 1]) {
            $temp = $w[$n];
            $w[$n] = $w[$n - 1];
            $w[$n - 1] = $temp;

            $swaps = true;
        }
    }
    if ($swaps == false) break;
}

echo "The three heaviest weights are: \n";
echo $w[ELEMENTS - 3], "\t", $w[ELEMENTS - 2], "\t", $w[ELEMENTS - 1], "\n";
echo "The three lightest weights are: \n";
echo $w[0], "\t", $w[1], "\t", $w[2], "\t";
?>
```

# Exercise 37.4-7 The Five Best Scorers

Write a PHP script that prompts the user to enter the names of the 32 national teams of the FIFA World Cup, the names of the 24 players for each team, and the total number of

