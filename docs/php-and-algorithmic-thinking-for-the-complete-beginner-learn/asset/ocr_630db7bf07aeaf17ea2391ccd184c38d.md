```
$x = sqrt($x) + $i;
echo $x, "\n";
}
```

# 16. Rewrite the following code fragment using the counted loop structure.

```
<?php
$p = 1;
$a = trim(fgets(STDIN));
$i = $a;
do {
	$p = $p * pow($i, 2);
	$i = $i + 5;
	$p = $p + $i;
} while ($i < 20);
echo $p;
?>
```

# 17. Rewrite the following code fragment using the counted loop structure.

```
<?php
$start = trim(fgets(STDIN));
$end = trim(fgets(STDIN));
$x = 1000;
$i = $start;
if ($i <= $end) {
	do {
		$x = sqrt($x);
		$i += 2;
	} while ($i <= $end);
}
echo $x;
?>
```

# 18. Write a PHP script that displays every combination of two integers as well as
their resulting product, for pairs of integers between 1 and 4. The output
should display as follows.

1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
1 x 4 = 4
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6