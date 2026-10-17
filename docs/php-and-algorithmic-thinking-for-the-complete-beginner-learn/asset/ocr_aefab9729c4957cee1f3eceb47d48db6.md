# The final PHP script is as follows.

```
```php
<?php
define("EVENTS", 20);
define("COUNTRIES", 10);

$country_names = array();
$event_descriptions = array(array());
$event_years = array(array());
for ($j = 0; $j <= COUNTRIES - 1; $j++) {
    echo "Enter Country No. ", $j + 1, ": ";
    $country_names[$j] = trim(fgets(STDIN));
    for ($i = 0; $i < EVENTS - 1; $i++) {
        echo "Enter description for event No. ", $i + 1, ": ";
        $event_descriptions[$i][$j] = trim(fgets(STDIN));
        echo "Enter year for event No. ", $i + 1, ": ";
        $event_years[$i][$j] = trim(fgets(STDIN));
    }
}

echo "Enter a year to search: ";
$needle = trim(fgets(STDIN));

for ($j = 0; $j <= COUNTRIES - 1; $j++) {
    $top = 0;
    $bottom = EVENTS - 1;
    $found = false;
    while ($top <= $bottom && $found == false) {
        $middle = intval(($top + $bottom) / 2);

        if ($event_years[$middle][$j] > $needle) {
            $bottom = $middle - 1;
        }
        elseif ($event_years[$middle][$j] < $needle) {
            $top = $middle + 1;
        }
    }
}
```
```