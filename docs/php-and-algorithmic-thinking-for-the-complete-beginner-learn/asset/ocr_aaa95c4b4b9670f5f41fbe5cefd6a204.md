This exercise uses a multiple-alternative decision structure and a dual-alternative decision structure nested inside the first one.

The PHP script is shown here.

```
```php
<?php
    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));


    $c = $a % 2;
    $d = intval($b / 5);


    if ($a >= $b)
        $y = 1;
    elseif ($d > $c && $a > 2)
        $y = 2;
    elseif ($d*$c > a / b) {
        if ($d * $c > 10)
            $y = 4;
        else
            $y = 3;
    }
    else
        $y = 5;

    echo $y;
?>
```
```

> This is the dual-alternative decision structure

# 22.4 Review Exercises

Complete the following exercises.

+   1. Design the flowchart that corresponds to the following PHP script.

```
```php
<?php
    $a = trim(fgets(STDIN));


    if ($a % 10 == 0) {
        $a++;
        echo "Message #1";
    }
    if ($a % 3 == 1) {
        $a += 5;
        echo "Message #2";
    }
}
```
```