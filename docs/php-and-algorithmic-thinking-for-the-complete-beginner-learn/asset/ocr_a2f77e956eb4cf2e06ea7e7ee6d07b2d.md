```
elseif ($os == "iOS") {
    echo "Apple";
}
elseif ($os == "Android") {
    echo "Google";
}
?>
```

10. Rewrite the following PHP script using the multiple-alternative decision structure.

```
<?php
$a = trim(fgets(STDIN));
$x = trim(fgets(STDIN));
$y = trim(fgets(STDIN));

switch ($a) {
    case 3:
        $x = $x / 4;
        $y = pow($y, 5);
        break;
    case 7:
        $x = $x * 3;
        $y++;
        break;
    case 22:
        $x = $x % 4;
        $y += 9;
        break;
    default:
        $x -= 9;
        $y++;
}

echo $x, $y;
?>
```

11. Rewrite the PHP script of the previous exercise using nested decision control structures.

12. Rewrite the following PHP script using the case decision structure.

```
<?php
echo "Enter a color in hexadecimal: ";
```