# ## Solution

Following is the script of the exercise, written again, with some notes on it.

```
```php
<?php
    $x = 2;

    for ($i = -4; $i <= 4; $i = $i + 1) {
        $x = pow($x, 2);
    }

echo $x;
?>
```
```

![](bbox=[0.052, 0.286, 0.822, 0.5])

Now, with everything clarified, the PHP script can be rewritten using the pre-test loop structure.

```
```php
<?php
    $x = 2;

    $i = -4;
    while ($i <= 4) {
        $x = pow($x, 2);
        $i = $i + 1;
    }

echo $x;
?>
```
```

If you type and execute both scripts in NetBeans IDE, you can find out for yourself that they both display the same result.