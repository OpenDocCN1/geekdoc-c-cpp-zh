```
}

$a++;

if ($a > 0) {
    echo "Hallo Welt";
}

echo $b;
?>
```

# 21.6 Replacing Two Single-Alternative Decision Structures with a Dual-Alternative One

Take a look at the next example.

```
if ($a > 40) {
    //do something
}

if ($a <= 40) {
    //do something else
}
```

The first decision control structure evaluates variable $a to test if it is bigger than 40, and right after that, a second decision control structure evaluates the same variable again to test if it is less than or equal to 40!

This is a very common “mistake” that novice programmers make. They use two single-alternative decision structures even though one dual-alternative decision structure can accomplish the same thing.

The previous example can be rewritten using only one dual-alternative decision structure, as shown here.

```
if ($a > 40) {
    //do something
}
else {
    //do something else
}
```

Even though both examples are absolutely correct and work perfectly well, the second alternative is better. The CPU needs to evaluate only one Boolean expression, which results in faster execution time.