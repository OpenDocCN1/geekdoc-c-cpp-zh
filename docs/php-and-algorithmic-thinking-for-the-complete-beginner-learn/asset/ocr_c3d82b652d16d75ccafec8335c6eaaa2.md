$a again to test if it is not greater than zero. Even though there is the statement $b = trim(fgets(STDIN)) between them, this statement can be moved somewhere else because it doesn't really affect the rest of the flow of execution.

On the other hand, between the third and fourth decision control structures there is the statement $y++ which also prevents you from merging. However, this statement cannot be moved anywhere else because it does affect the rest of the flow of execution (the third and fourth decision control structures are dependent upon this statement). Therefore, the third and fourth decision control structures cannot be merged!

The final PHP script becomes

```
<?php
    $a = trim(fgets(STDIN));
    $b = trim(fgets(STDIN));

    $y = 0;

    if ($a > 0) {
        $y++;
    }
    else {
        echo "Hello Zeus";
    }

    if ($y > 0) {
        echo $y + 5;
    }

    $y++;

    if ($y <= 0) {
        echo $y + 12;
    }
?>
```

# 21.7 Put the Boolean Expressions Most Likely to be True First

Both the multiple-alternative and the case decision structure often need to check several Boolean expressions before deciding which statement or block of statements to execute. In the next decision control structure,

```
if (Boolean_Expression 1) {
    A statement or block of statements 1
}
```