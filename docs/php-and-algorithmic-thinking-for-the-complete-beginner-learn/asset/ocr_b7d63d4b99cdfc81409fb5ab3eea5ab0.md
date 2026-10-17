```
```php
$x2 = (-$b - sqrt($D)) / (2 * $a);
echo "Roots: ", $x1, ", ", $x2;
}
else {
    $x = -$b / (2 * $a);
    echo "One double root: ", $x;
}
}
else {
    echo "Complex Roots";
}
}
else {
    if ($b != 0) {
        $x = -$c / $b;
        echo "Root: ", $x;
    }
    elseif ($c != 0) {
        echo "Undefined";
    }
    else {
        echo "Indeterminate form";
    }
}
?>
```
```

# 23.3 Finding Minimum and Maximum Values with Decision Control Structures

Suppose there are some men and you want to find the lightest one. Let’s say that each one of them comes by and tells you his weight. What you must do is, memorize the weight of the first person that has come by and for each new person, you have to compare his weight with the one that you keep memorized. If he is heavier, you ignore his weight. However, if he is lighter, you need to forget the previous weight and memorize the new one. The same procedure continues until all the people have come by.

Let’s ask four men to come by at a random order. Assume that their weights, in order of appearance, are 165, 170, 160, and 180 pounds.