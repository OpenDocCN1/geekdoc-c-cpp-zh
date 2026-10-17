![](bbox=[0.05, 0.05, 0.95, 0.55])

# ## Solution

This flowchart has one single-decision structure nested within a pre-test loop structure, which in turn is nested within another pre-test loop structure.

Since variables i and j are used as index positions for array a, you can assume that they are integers. Therefore, it is permitted to alter the two Boolean expressions to i <= CITIES - 1 and j <= CITIZENS - 1, respectively. This change helps you write the corresponding PHP script using counted loop structures, as follows.

```
```php
$max_i = 0;
$max_j = 0;
for ($i = 0; $i <= CITIES - 1; $i++) {
    for ($j = 0; $j <= CITIZENS - 1; $j++) {
        if ($a[$i][$j] > $a[$max_i][$max_j]) {
            $max_i = $i;
            $max_j = $j;
        }
    }
}
```
```