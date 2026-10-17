```
```php
$t = array();
for ($i = 0; $i <= DAYS - 1; $i++) {
    $t[$i] = trim(fgets(STDIN));
}
```
```

```
```php
$count = 0;
for ($i = 0; $i <= DAYS - 1; $i++) {
    if ($t[$i] < 36) {
        $count++;
    }
}
```
```

```
```php
if ($count != 0) {
    echo "There was a possibility of snow in January!";
}
```
```

# ## Second Approach – Using a flag

In this approach, instead of counting all those days that had a temperature below 36 degrees Fahrenheit, you can use a Boolean variable (a flag). The solution is presented next.

```
```php
<?php
define("DAYS", 31);
$t = array();
for ($i = 0; $i <= DAYS - 1; $i++) {
    $t[$i] = trim(fgets(STDIN));
}
$found = false;
for ($i = 0; $i <= DAYS - 1; $i++) {
    if ($t[$i] < 36) {
        $found = true;
    }
}
if ($found == true) {
    echo "There was a possibility of snow in January!";
}
```
```