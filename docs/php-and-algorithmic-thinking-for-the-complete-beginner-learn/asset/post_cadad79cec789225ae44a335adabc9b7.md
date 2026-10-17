

## Second Approach - Using a flag

This book tries to use the `break` statement as little as possible, and only in certain situations in which it really helps you make your code better. That's because the `break` statement doesn't actually exist in all computer languages; and since this book's intent is to teach you “Algorithmic Thinking” (and not just special statements that only PHP supports), let's look at an alternate approach.

To break out of a loop using a flag, there is one methodology that you can always follow: the counted loop structure must be converted to a pre-test loop structure, and the Boolean expression of the loop must be modified to evaluate an extra variable. In the next code fragment this extra variable is the variable `$found` which, when the given value is found within array `$haystack`, forces the flow of execution to immediately exit the loop.

```php
echo "Enter a value to search: ";
$needle = trim(fgets(STDIN));

$found = false;
$i = 0;
while ($i <= ELEMENTS - 1 && $found == false) {
    if ($haystack[$i] == $needle) {
        $found = true;
        $index_position = $i;
    }
    $i++;
}

if ($found == false) {
    echo "Nothing found!";
}
else {
    echo $needle, " found at position: ", $index_position;
}
```

## Third Approach – Using only a pre-test loop structure

This approach is probably the most efficient one. Also, it is so easy to understand the way is works that there is no need to explain anything. The code fragment is as follows.

```php
echo "Enter a value to search: ";
$needle = trim(fgets(STDIN));

$i = 0;
while ($i < ELEMENTS - 1 && $haystack[$i] != $needle) {
	$i++;
}

if ($haystack[$i] != $needle) {
	echo "Nothing found!";
}
else {
	echo $needle, " found at position: ", $i;
}
```

## Exercise 37.5-4 Searching for a Given Social Security Number

In the United States, the Social Security Number (SSN) is a nine-digit identity number applied to all U.S. citizens in order to identify them for the purposes of Social Security. Write a PHP script that prompts the user to enter the SSN and the first and last names of 100 people. The script should then ask the user for an SSN, upon which it will search and display the first and last name of the person who holds that SSN.

## Solution

According to everything you learned so far, the solution to this exercise is as follows.

```php
<?php
define("PEOPLE", 100);

$SSNs = array();
$first_names = array();
$last_names = array();
for ($i = 0; $i <= PEOPLE - 1; $i++) {
	echo "Enter SSN: ";
	$SSNs[$i] = trim(fgets(STDIN));
	echo "Enter first name: ";
	$first_names[$i] = trim(fgets(STDIN));
	echo "Enter last name: ";
	$last_names[$i] = trim(fgets(STDIN));
}
echo "Enter an SSN to search: ";
$needle = trim(fgets(STDIN));
$i = 0;
while ($i < PEOPLE - 1 && $SSNs[$i] != $needle) {
    $i++;
}
if ($SSNs[$i] != $needle) {
    echo "Nothing found!";
} else {
    echo $first_names[$i], ", ", $last_names[$i];
}
?>
```

**Notice:** In the United States, there is no possibility that two or more people will have the same SSN. Thus, even though it is not very clear in the wording of the exercise, each value in array $SSNs is unique!

## Exercise 37.5-5 Searching in a Two-Dimensional Array that may Contain the Same Value Multiple Times

Twelve teams participate in a football tournament, and each team plays 20 games, one game each week. Write a PHP script that prompts the user to enter the name of each team and the letter “W” for win, “L” for loss, or “T” for tie (draw) for each game. Then the script should prompt the user for a letter (W, L, or T) and display, for each team, the week number(s) in which the team won, lost, or tied respectively. For example, if the user enters “L,” the PHP script should search and display, for each team, the week numbers (e.g., week 3, week 14, and so on) in which the team lost the game.

## Solution

In this exercise, you need the following two arrays.

# Chapter 37
More Exercises with Arrays

The corresponding PHP script is as follows.

```php
<?php
define("TEAMS", 20);
define("WEEKS", 12);

$names = array();
$results = array(array());
for ($i = 0; $i <= TEAMS - 1; $i++) {
    echo "Enter name for team No. ", $i + 1, ": ";
    $names[$i] = trim(fgets(STDIN));
    for ($j = 0; $j <= WEEKS - 1; $j++) {
        echo "Enter result for week No. ", $j + 1, " for ", $names[$i], ": ";
        $results[$i][$j] = trim(fgets(STDIN));
    }
}

echo "Enter a result to search: ";
$needle = trim(fgets(STDIN));

for ($i = 0; $i <= TEAMS - 1; $i++) {
    $found = false;
    echo "Found results for ", $names[$i], "\n";
    for ($j = 0; $j <= WEEKS - 1; $j++) {
        if (strtoupper($results[$i][$j]) == strtoupper($needle)) {
            echo "Week No ", $j + 1, "\n";
            $found = true;
        }
    }
    if ($found == false) {
        echo "No results!\n";
    }
}
?>
```

## Exercise 37.5-6 Searching in a Two-Dimensional Array that Contains Unique Values

A public opinion polling company makes phone calls in 10 cities and asks 30 citizens in each city whether or not they exercise. Write a PHP script that prompts the user to enter each citizen’s phone number and their answer (Y for Yes, N for No, S for Sometimes). The script should then prompt the user to enter a phone number, and it will search and display the answer that was given at this phone number. The script should also validate data input and accept only the values Y, N, or S as an answer.

## Solution

In this exercise, you need the following two arrays.

# Chapter 37
More Exercises with Arrays

The corresponding PHP script is as follows.

```php
file_37.5-6.php
<?php
define("CITIES", 10);
define("CITIZENS", 30);
$phone_num = array(array());
$ans = array(array());
for ($i = 0; $i <= CITIES - 1; $i++) {
echo "City No. ", $i + 1, "\n";
for ($j = 0; $j <= CITIZENS - 1; $j++) {
echo "Enter phone number of citizen No. ", $j + 1, ": ";
$phone_num[$i][$j] = trim(fgets(STDIN));

echo "Enter the answer of citizen No. ", $j + 1, ": ";
$ans[$i][$j] = strtoupper(trim(fgets(STDIN)));
while ($ans[$i][$j] != "Y" &&
       $ans[$i][$j] != "N" &&
       $ans[$i][$j] != "S") {
    echo "Wrong answer. Please enter a valid answer: ";
    $ans[$i][$j] = strtoupper(trim(fgets(STDIN)));
}

}
}

echo "Enter a phone number to search: ";
$needle = trim(fgets(STDIN));

$found = false;
$i = 0;
while ($i <= CITIES - 1 && $found == false) {
    $j = 0;
    while ($j <= CITIZENS - 1 && $found == false) {
        if ($phone_num[$i][$j] == $needle) {
            $found = true;
            $position_i = $i;
            $position_j = $j;
        }
        $j++;
    }
    $i++;
}

if ($found == false) {
    echo "Phone number not found!";
}
else {
    echo "Phone number ", $phone_num[$position_i][$position_j], " gave ";

    switch ($ans[$position_i][$position_j]) {
        case "Y":
echo "Yes";
break;
case "N":
echo "No";
break;
default:
echo "Sometimes";
}
echo "' as an answer";
}
?>
```

## Exercise 37.5-7 Checking if a Value Exists in all Columns

Write a PHP script that lets the user enter numeric values into a 20 × 30 array. After all of the values have been entered, the script then lets the user enter a value. A message should be displayed if the given value exists, at least once, in each column of the array.

## Solution

This exercise can be solved using the linear search algorithm and a counter variable $count. The PHP script can iterate through the first column and if the given value is found, the variable $count should increment by one. Then the script can iterate through the second column and if the given value is found again, the variable $count should again increment by one. This process should repeat until all columns have been examined. At the end of the process, if the value of $count is equal to the total number of columns, this means that the given value exists, at least once, in each column of the array.

Let’s use the “from inner to outer” method. The following code fragment searches in first column (column index 0) of the array and if the given value is found, variable $count increments by one. Assume variable $j contains the value 0.

```php
$found = false;
$i = 0;
while ($i <= ROWS - 1 && $found == false) {
if ($haystack[$i][$j] == $needle) {
$found = true;
}
$i++;
}
if ($found == true) {
$count++;
```

