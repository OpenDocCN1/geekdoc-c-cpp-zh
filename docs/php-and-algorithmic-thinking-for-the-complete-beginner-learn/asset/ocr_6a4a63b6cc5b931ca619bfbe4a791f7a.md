One proposed solution is presented next. If you still have doubts about how this operates, you can use NetBeans IDE to execute it step by step and observe the values of the variables in each step.

```
```php
<?php
echo "Enter a message: ";
$message = trim(fgets(STDIN));

//Convert all letters to lowercase
$message = strtolower($message);

//This is the last position of $message
$last_pos = strlen($message) - 1;

//Create a new string which contains letters except
//spaces, commas, periods or questionmarks
$message_clean = "";
for ($i = 0; $i <= $last_pos; $i++) {
    if ($message[$i] != " " && $message[$i] != "," &&
        $message[$i] != "." && $message[$i] != "?") {

        $message_clean .= $message[$i];
    }
}

//This is the middle position of $message_clean
$middle_pos = intval((strlen($message_clean) - 1) / 2);

//This is the last position of $message_clean
$j = strlen($message_clean) - 1;

//In the beginning, assume that sentence is palindrome
$palindrome = true;

//This counted loop structure compares
//letters one by one.
for ($i = 0; $i <= $middle_pos; $i++) {
```
```

This code fragment can be further improved as you can see next.