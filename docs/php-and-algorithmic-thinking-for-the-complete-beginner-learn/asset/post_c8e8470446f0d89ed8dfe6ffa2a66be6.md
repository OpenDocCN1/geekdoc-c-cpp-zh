
## Chapter 27
Counted Loop Structures

```
}
}
echo $b;
?>
```

- 3. Create a trace table to determine the values of the variables in each step of the next PHP script for the input value 12.

```php
<?php
    $a = trim(fgets(STDIN));
    for ($j = 2; $j <= $a - 1; $j += 3) {
        $x = $j * 3 + 3;
        $y = $j * 2 + 10;
        if ($y - $x > 0 || $x > 30) {
            $y *= 2;
        }
        $x += 4;
        echo $x, $y;
    }
?>
```

- 4. Fill in the gaps in the following code fragments so that all loops perform exactly five iterations.

- i.
```php
for ($a = 5; $a <= ......; $a++) {
    $b++;
}
```

- ii.
```php
for ($a = 0; $a <= ......; $a += 0.5) {
    $b++;
}
```

- iii.
```php
for ($a = ......; $a >= -15; $a -= 2) {
    $b++;
}
```

- iv.
```php
for ($a = -11; $a >= -15; $a = $a ......) {
    $b++;
}
```

- 5. Design a flowchart and write the corresponding PHP script that prompts the user to enter 20 numbers and then calculates and displays their product and their average value.

- 6. Write a PHP script that prompts the user to enter a number in degrees and then calculates and displays the sinus of all numbers from 0 to that given number, using an offset of 0.5. It is given that 2π = 360°.

- 7. Design a flowchart and write the corresponding PHP script that prompts the user to enter 30 four-digit integers and then calculates and displays the sum of those with a first digit of 5 and a last digit of 3. For example, values 5003, 5923, and 5553 are all such integers.

- 8. Design a flowchart and write the corresponding PHP script that prompts the user to enter N integers and then displays the total number of those that are even. The value of N should be given by the user at the beginning of the script. Moreover, if all integers given are odd, the message “You entered no even integers” should be displayed.

- 9. Design a flowchart and write the corresponding PHP script that prompts the user to enter 50 integers and then calculates and displays the average value of those that are odd and the average value of those that are even.

- 10. Design a flowchart and write the corresponding PHP script that prompts the user to enter two integers into variables `$start` and `$finish` and then displays all integers from `$start` to `$finish`. However, at the beginning the script should check if variable `$start` is bigger than variable `$finish`. If this happens, the script should swap their values so that they are always in the proper order.

- 11. Design a flowchart and write the corresponding PHP script that prompts the user to enter two integers into variables `$start` and `$finish` and then displays all integers from `$start` to `$finish` that are multiples of five. However, at the beginning the script should check if variable `$start` is bigger than variable `$finish`. If this happens, the script should swap their values so that they are always in the proper order.

- 12. Write a PHP script that prompts the user to enter a real and an integer and then displays the result of the first number raised to the power of the second number, without using the `pow()` function.

- 13. Write a PHP script that prompts the user to enter a message and then displays the number of words it contains. For example, if the string entered is “My name is Bill Bouras”, the script should display “The message entered contains 5 words”. Assume that the words are separated by a single space character.

Hint: Use the `strlen()` function to get the number of characters that the given message contains.

- 14. Write a PHP script that prompts the user to enter any string and then displays the average number of letters in each word. For example, if the string entered is “My name is Aphrodite Boura”, the script should display “The average number of letters in each word is 4.4”. Space characters should not be counted.

## Chapter 28
### Nested Loop Control Structures

### 28.1 What is a Nested Loop?

A nested loop is a loop within another loop or, in other words, an inner loop within an outer one.

The outer loop controls the number of complete iterations of the inner loop, which means that the first iteration of the outer loop triggers the inner loop to start iterating until completion. Then the second iteration of the outer loop triggers the inner loop to start iterating until completion again. This process repeats until the outer loop has performed all of its iterations.

Take the following PHP script, for example.

```php
file_28.1.php
for ($i = 1; $i <= 2; $i++) {
  for ($j = 1; $j <= 3; $j++) {
    echo $i, " ", $j, "\n";
  }
}
```

The outer loop, the one that is controlled by variable $i, controls the number of complete iterations that the inner loop performs. That is, when variable $i contains the value 1, the inner loop performs three iterations (for $j = 1, $j = 2, and $j = 3). The inner loop finishes but the outer loop needs to perform one more iteration (for $i = 2), so the inner loop starts over and performs three new iterations again (for $j = 1, $j = 2 and $j = 3).

The previous example can be likened to the following one.

```php
$i = 1; //outer loop assigns value 1 to variable $i
for ($j = 1; $j <= 3; $j++) { //and inner loop performs three iterations
  echo $i, " ", $j, "\n";
}

$i = 2; //outer loop assigns value 2 to variable $i
for ($j = 1; $j <= 3; $j++) { //and inner loop starts over and
  echo $i, " ", $j, "\n"; //performs three new iterations
}
```

The output result is as follows.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_425_0.png)

> **Remember!** As long as the syntax rules are not violated, you can nest as many loop control structures as you wish. For practical reasons however, as you move to four or five levels of nesting, the entire loop structure becomes very complex and difficult to understand. However, experience shows that the maximum levels of nesting that you will do in your entire life as a programmer is probably three or four.
>
> **Notice:** There is no need for the inner and outer loops to be of the same type. For example, a `for` statement may nest (enclose) a `while` statement, or vice versa.

### Exercise 28.1-1 Say “Hello Zeus”. Designing the Flowchart and Counting the Total Number of Iterations

Design the corresponding flowchart for the next code fragment, and find the number of times message “Hello Zeus” is displayed.

```php
for ($i = 1; $i <= 4; $i++) {
    for ($j = 1; $j <= 3; $j++) {
        echo "Hello Zeus\n";
    }
}
```

# Solution

The corresponding flowchart is as follows. The inner loop is marked with a dashed rectangle.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_426_0.png)

```php
for ($j = 1; $j <= 3; $j++) {
    echo "Hello Zeus\n";
}
```

Now, let’s try to count the number of times message “Hello Zeus” is displayed. By studying the corresponding flowchart you can see that the values of variables i and j (in order of appearance) are as follows:

- For i = 1, the inner loop performs 3 iterations (for j = 1, j = 2, and j = 3) and the message “Hello Zeus” is displayed 3 times.
- For i = 2, the inner loop performs 3 iterations (for j = 1, j = 2, and j = 3) and the message “Hello Zeus” is displayed 3 times.
- For i = 3, the inner loop performs 3 iterations (for j = 1, j = 2, and j = 3) and the message “Hello Zeus” is displayed 3 times.
- For i = 4, the inner loop performs 3 iterations (for j = 1, j = 2, and j = 3) and the message “Hello Zeus” is displayed 3 times.

Therefore, the message “Hello Zeus” is displayed a total of 4 × 3 = 12 times.

> **Remember!** The outer loop controls the number of complete iterations of the inner one!

### Exercise 28.1-2 Creating the Trace Table

Design the corresponding flowchart for the next code fragment, and determine the value that variable $a contains at the end.

```php
$a = 1;
$i = 5;

while ($i < 7) {
    for ($j = 1; $j <= 3; $j += 2) {
        $a = $a * $j + $i;
    }
    $i++;
}
echo $a;
```

# Solution

Following is the corresponding flowchart. The inner loop is marked with a dashed rectangle.

![](img/4d9a992abc5da7946ac44f9e6bf1d032_427_0.png)

With the help of the flowchart you can now create the following trace table.

| Step | Statement | Notes | $a | $i | $j |
|---:|---|---|---:|---:|---:|
| 1 | `$a = 1` |  | **1** | ? | ? |
| 2 | `$i = 5` |  | 1 | **5** | ? |
| 3 | `$i < 7` | This evaluates to *true* |  |  |  |
| 4 | `$j = 1` |  | 1 | 5 | **1** |
| 5 | `$j <= 3` | This evaluates to *true* |  |  |  |
| 6 | `$a = $a * $j + $i` |  | **6** | 5 | 1 |
| 7 | `$j = $j + 2` |  | 6 | 5 | **3** |
| 8 | `$j <= 3` | This evaluates to *true* |  |  |  |
| 9 | `$a = $a * $j + $i` |  | **23** | 5 | 3 |
