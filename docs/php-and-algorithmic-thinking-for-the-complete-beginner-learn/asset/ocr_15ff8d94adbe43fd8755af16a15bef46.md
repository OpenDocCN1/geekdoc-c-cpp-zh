```
```php
echo "Three lowest values are: " . $low[0] . ", " . $low[1] . ", " . $low[2] . "\n";

//In this step, array $t is NOT sorted
for ($i = 0; $i <= ELEMENTS - 1; $i++) {
    echo $t[$i], "\t", $names[$i], "\n";
}
?>
```
```

> **Notice:** Returning an array from a subprogram is as easy as returning a simple variable.

# 4.1.5 Default Argument Values (Optional Arguments)

If you assign a default value to an argument within the formal argument list, it means that if no value is passed for that argument, the default value is used. In the next example, the function `prepend_title()` prepends a title before the name. However, if no value for argument `$title` is passed, the function uses the default value “Mr.”

```
```php
<?php
function prepend_title($name, $title = "Mr") {
    return $title . " " . $name;
}

echo prepend_title("John King");        //It displays Mr John King
echo prepend_title("Maria Miller", "Ms"); //It displays Ms Maria Miller
?>
```
```

> **Notice:** When a default value is assigned to an argument within the formal argument list, this argument is called an optional argument.

Within the formal argument list, any optional arguments should be on the right side of any non-optional arguments; to do the opposite of this would be incorrect. Consider the following example, in which the optional argument `$title` is written before the non-optional argument `$name` in the formal argument list.

```
```php
<?php
function prepend_title($title = "Mr", $name) {
    return $title . " " . $name;
}

echo prepend_title("Vassilis Bouras");
?>
```
```