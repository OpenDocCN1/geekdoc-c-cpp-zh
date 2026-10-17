

## Exercise 37.2-2 Displaying Odds in Reverse Order - Validation with One Error Message

Write a PHP script that prompts the user to enter 20 odd integers into an array and then displays them in reverse order. The script should also validate data input and display an error message when the user enters any non-numeric values or any even integers.

### Solution

This is the same as you’ve previously seen, except for data validation. The second approach is used, according to which an error message is displayed when the user enters even integers. The PHP script is presented next.

```php
<?php
define("ELEMENTS", 20);

$odds = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    echo "Enter an odd integer: ";
    $odds[$i] = trim(fgets(STDIN));
    while (is_numeric($odds[$i]) != true || $odds[$i] % 2 == 0) {
        echo "Invalid value! \n";
        echo "Enter an odd integer: ";
        $odds[$i] = trim(fgets(STDIN));
    }
}

// display elements backwards
for ($i = ELEMENTS - 1; $i >= 0; $i--) {
    echo $odds[$i], "\t";
}
?>
```

## Exercise 37.2-3 — Displaying Odds in Reverse Order – Validation with Individual Error Messages

Write a PHP script that prompts the user to enter 20 odd integers in an array and then displays them in reverse order. The script should also validate data input and display individual error messages when the user enters any non-numeric values, any even integers, or any reals.

### Solution

The third approach is used, according to which individual error messages are displayed when the user enters non-numeric values, even integers, or reals. The PHP script is as follows.

```php
<?php
define("ELEMENTS", 20);

$odds = array();
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    do {
        echo "Enter an odd integer: ";
        $odds[$i] = trim(fgets(STDIN));
        $failure = false;
        if (is_numeric($odds[$i]) != true) {
            echo "Please enter a numeric value! \n";
            $failure = true;
        }
        elseif ($odds[$i] != intval($odds[$i])) {
            echo "Please enter an integer! \n";
            $failure = true;
        }
        elseif ($odds[$i] % 2 == 0) {
            echo "Please enter an odd! \n";
            $failure = true;
        }
    } while ($failure == true);
}

// display elements backwards
for ($i = ELEMENTS - 1; $i >= 0; $i--) {
    echo $odds[$i], "\t";
}
?>
```

## 37.3 Finding Minimum and Maximum Values in Arrays

This is the third and last time that this subject is raked up in this book. The first time was in Section 4 (Decision Control Structures) and the second time was in Section 5 (Loop Control Structures). So, there is not much left to discuss except that when you want to find the minimum or maximum value of an array that already contains some values, you needn't worry about the initial values of variables $min or $max because you can just assign to them the value of the first element of the array!

### Exercise 37.3-1 Which Depth is the Greatest?

Design a flowchart and write the corresponding PHP script that lets the user enter the depths of 20 lakes and then displays the depth of the deepest one.

### Solution

After the user enters the depths of the 20 lakes in the array $depths, the initial value of variable $max can be set as the value of the first element of array $depths, that is $depths[0]. The script can then search for any value greater than this. The final solution is quite simple and is presented next without further explanation.

### Exercise 37.3-2 Which Lake is the Deepest?

Write a PHP script that lets the user enter the names and the depths of 20 lakes and then displays the name of the deepest one.

### Solution

In this exercise, you need two one-dimensional arrays: one to hold the names, and one to hold the depths of the lakes. The solution is presented next.

```php
<?php
define("LAKES", 20);

$names = array();
$depths = array();
for ($i = 0; $i <= LAKES - 1; $i++) {
    $names[$i] = trim(fgets(STDIN));
    $depths[$i] = trim(fgets(STDIN));
}

$max = $depths[0];
$m_name = $names[0];
for ($i = 1; $i <= LAKES - 1; $i++) {
    if ($depths[$i] > $max) {
        $max = $depths[$i];
        $m_name = $names[$i];
    }
}

echo $m_name;
?>
```

### Exercise 37.3-3 Which Lake, in Which Country, Having Which Average Area, is the Deepest?

Write a PHP script that lets the user enter the names and the depths of 20 lakes as well as the country in which they belong, and their average area. The script should then display all available information about the deepest lake.

### Solution

In this exercise, you need four one-dimensional arrays: one to hold the names, one to hold the depths, one to hold the names of the countries, and one to hold the lakes’ average areas. There are two approaches, actually. The first one is pretty much the same as the one used in the previous exercise. The second one is more efficient since it uses fewer variables. Let’s study them both!

#### First Approach – One variable for each

This is pretty much the same as the one used in the previous exercise. The solution is presented next.

```php
<?php
define("LAKES", 20);

$names = array();
$depths = array();
$countries = array();
$areas = array();
for ($i = 0; $i <= LAKES - 1; $i++) {
    $names[$i] = trim(fgets(STDIN));
    $depths[$i] = trim(fgets(STDIN));
    $countries[$i] = trim(fgets(STDIN));
    $areas[$i] = trim(fgets(STDIN));
}

$max = $depths[0];
$m_name = $names[0];
$m_country = $countries[0];
$m_area = $areas[0];
for ($i = 1; $i <= LAKES - 1; $i++) {
    if ($depths[$i] > $max) {
        $max = $depths[$i];
        $m_name = $names[$i];
        $m_country = $countries[$i];
        $m_area = $areas[$i];
    }
}

echo $max, $m_name, $m_country, $m_area;
?>
```

#### Second Approach – One index for everything

In this approach fewer variables are used. Instead of using all those variables ($m_name, $m_country, and $m_area), you can use just one variable, a variable that holds the index in which the maximum value exists!

Confused? Let’s look at the next example of six lakes. The depths are expressed in feet and the average areas in square miles.

| Index | $names | $depths | $countries | $areas |
|---:|---|---:|---|---:|
| 0 | Toba | 1660 | Indonesia | 440 |
| 1 | Issyk Kul | 2192 | Kyrgyzstan | 2408 |
| 2 | Baikal | 5380 | Russia | 12248 |
| 3 | Crater | 1950 | USA | 21 |
| 4 | Karakul | 750 | Tajikistan | 150 |
| 5 | Quesnel | 2000 | Canada | 103 |

Obviously the deepest lake is Lake Baikal at position 2. However, instead of holding the name “Baikal” in variable $m_name, the country “Russia” in variable $m_country, and the area “12248” in variable $m_area as in the previous approach, you can use just one variable to hold the index position in which these values actually exist (in this case, this is value 2). The solution is presented next.

```php
<?php
define("LAKES", 20);

$names = array();
$depths = array();
$countries = array();
$areas = array();
for ($i = 0; $i <= LAKES - 1; $i++) {
    $names[$i] = trim(fgets(STDIN));
    $depths[$i] = trim(fgets(STDIN));
    $countries[$i] = trim(fgets(STDIN));
    $areas[$i] = trim(fgets(STDIN));
}

$max = $depths[0];
$index_of_max = 0;
for ($i = 1; $i <= LAKES - 1; $i++) {
    if ($depths[$i] > $max) {
        $max = $depths[$i];
        $index_of_max = $i;
    }
}

echo $depths[$index_of_max], $names[$index_of_max];
echo $countries[$index_of_max], $areas[$index_of_max];
?>
```

> **Remember!** Assigning an initial value of 0 to variable `$index_of_max` is necessary since there is always a possibility that the maximum value does exist in position 0.

### Exercise 37.3-4 Which Students are the Tallest?

Write a PHP script that prompts the user to enter the names and the heights of 100 students and then displays the names of all those who share the one tallest height. Moreover, the script should validate data input and display an error message when the user enters any non-numeric or negative values.

### Solution

In this exercise, a loop control structures should search for the greatest value, and afterwards, another loop control structure can search the array for all values that are equal to that greatest value.

The solution is presented next.

```php
<?php
    define("STUDENTS", 100);

    $names = array();
    $grades = array();
    for ($i = 0; $i <= STUDENTS - 1; $i++) {
        echo "Enter name for student No: ", $i + 1;
        $names[$i] = trim(fgets(STDIN));

        echo "Enter his or her grade: ";
        $grades[$i] = trim(fgets(STDIN));
        while (is_numeric($grades[$i]) != true || $grades[$i] < 0) {
            echo "Invalid value!";
            echo "Enter his or her grade: ";
            $grades[$i] = trim(fgets(STDIN));
        }
    }
?>
```

