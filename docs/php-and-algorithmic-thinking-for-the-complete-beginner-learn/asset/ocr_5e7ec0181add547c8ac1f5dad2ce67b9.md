```
$y = 3;
if ($a > 0) {
    $y = $y * $a;
}
$b = trim(fgets(STDIN));
if (!($a <= 0)) {
    echo "Hello Zeus";
}

echo $y, $b;
?>
```

8. In the following PHP script, “merge” the single-alternative decision structures.

```
<?php
$a = trim(fgets(STDIN));

$y = 0;
if ($a > 0) {
    $y = $y + 7;
}
$b = trim(fgets(STDIN));
if (!($a > 0)) {
    echo "Hello Zeus";
}
if ($a <= 0) {
    echo abs($a);
}
echo $y;
?>
```

9. According to research from 2013, the most popular operating system on tablet computers was iOS, with Android being in second place and Microsoft Windows in last place. In the following PHP script, rearrange the Boolean expressions to make the script run more efficiently for most of the cases.

```
<?php
echo "What is your tablet's OS? ";
$os = trim(fgets(STDIN));

if ($os == "Windows") {
    echo "Microsoft";
}
```