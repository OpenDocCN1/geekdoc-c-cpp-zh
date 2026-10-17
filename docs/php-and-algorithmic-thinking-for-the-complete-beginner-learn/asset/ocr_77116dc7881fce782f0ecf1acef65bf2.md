```
if ($x == 3) {
    echo "Hello and goodbye!";
}
else {
    echo "Gooooooood morning NY!";
}
}
}
?>
```

# Solution

Once again, this is a case in which you can't proceed with the conversion because there are some statements (in bold) existing between else and if keywords.

# 21.11 What is Code Indentation and Why is it so Important?

As you've been reading through this book, you may wonder why space characters appear in front of the PHP statements and why these statements are not written at the leftmost edge of the paragraph, as in the following example.

```
<?php
echo "Enter a number: ";
$x = trim(fgets(STDIN));
echo "Enter a second number: ";
$y = trim(fgets(STDIN));
if ($x > 5) {
echo "Variable x is greater than 5";
}
else {
$x = $x + $y;
echo "Hello Zeus!";
if ($x == 3) {
echo "Variable x equals to 3";
}
else {
$x = $x - $y;
echo "Hello Olympians!";
if ($x + $y == 24) {
echo "The sum of x + y equals to 24";
}
else {
echo "Nothing of the above";
```