![](bbox=[0.245, 0.06, 0.79, 0.255])

**Figure 6–2** The output result displays on one line

In order to output a “line break” you must put the special sequence of characters `\n` after every sentence.

```
```php
<?php
    echo "Good Morning\n";
    echo "Good Evening\n";
    echo "Good Night\n";
?>
```
```

The output result now appears in **Figure 6–3**.

![](bbox=[0.245, 0.487, 0.79, 0.677])

**Figure 6–3** The output result now displays line breaks

Keep in mind that the same result can be accomplished with one single statement.

```
```php
echo "Good Morning\nGood Evening\nGood Night\n";
```
```

Another interesting sequence of characters is the `\t` which can be used to output a “tab stop.” The tab character (`\t`) is useful for aligning output.

```
```php
<?php
    echo "Good Morning\t";
    echo "Good Evening\n";
    echo "Good Afternoon\t";
    echo "Good Night";
?>
```
```

The output result now appears in **Figure 6–4**.