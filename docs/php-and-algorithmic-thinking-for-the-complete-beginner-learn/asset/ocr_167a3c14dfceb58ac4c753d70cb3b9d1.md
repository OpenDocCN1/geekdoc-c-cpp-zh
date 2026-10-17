# # Chapter 29 Tips and Tricks with Loop Control Structures

```
```php
<?php
$a = trim(fgets(STDIN));
$b = trim(fgets(STDIN));
while ($b <= $a) {
    $a += 2;
    echo $a, ":", $b;
    $b = $b + 5;
}
?>
```
```

Suppose the user enters the values 14 and 10 for variables $a and $b respectively. For these values, both scripts perform two iterations and both display 16:10 and 18:15 on screen. They seem to produce the same results, but do they?

Let's try another pair of input values. Suppose the user enters the values 2 and 3 for variables $a and $b respectively. In this case, the post-test loop structure performs one iteration as opposed to the pre-test loop structure, which never enters the loop. Thus, it performs zero iterations!

So, in order to avoid this kind of problem and to be sure that your conversions are always correct, you should always go by the book. In any case, this is what rules are for!

# ## Exercise 29.9-2 Converting the PHP Script

Rewrite the following PHP script using the pre-test loop structure.

```
```php
<?php
$a = 0;
do {
    $b = trim(fgets(STDIN));
    $a = $a + $b;
} while ($a <= pow($b, 2));
echo $a;
?>
```
```

# ## Solution

No questions, no buts. Just follow the rule! The PHP script using the pre-test loop structure becomes

```
```php
<?php
```
```