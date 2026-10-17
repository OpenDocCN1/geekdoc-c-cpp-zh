```
}
elseif ($y < 20) {
    $x = $x * 5;
    $y += 2;
}
else {
    $x = $x - 2;
    $y += 3;
}
}
else {
    if ($y < 15) {
        $x = $x % 4;
        $y = 2;
    }
    elseif ($y < 23) {
        $x = $x % 2;
        $y -= 2;
    }
    else {
        $x = 2 * $x + 5;
        $y += 1;
    }
}

echo $x, $y;
?>
```

3. Write a PHP script that prompts the user to enter the lengths of three sides of a triangle, and then determines whether or not the given numbers can be lengths of the three sides of a triangle. If the lengths are not valid, a corresponding message should be displayed; otherwise the script should further determine whether the triangle is

+   a. equilateral
+      Hint: In an equilateral triangle, all sides are equal.
+   b. right (or right-angled)
+      Hint: Use the Pythagorean theorem.
+   c. not special
+      Hint: In any triangle, the length of each side is less than the sum of the lengths of the other two sides.