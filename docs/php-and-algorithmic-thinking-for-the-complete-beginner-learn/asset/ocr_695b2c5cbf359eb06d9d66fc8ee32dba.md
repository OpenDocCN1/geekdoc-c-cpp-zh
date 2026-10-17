This returns the *string*, converted to lowercase.

# Example

```
```php
<?php

$a = "My Name is JoHN";

$b = strtolower($a);

echo $b; //Outputs: my name is john
?>
```
```

# To uppercase

```
`strtoupper(string)`
```

This returns the *string*, converted to uppercase.

# Example

```
```php
<?php

$a = "My Name is JoHN";

$b = strtoupper($a);

echo $b; //Outputs: MY NAME IS JOHN
?>
```
```

# Getting part of a string

```
`substr(string, start [, length])`
```

This returns a portion of *string*. Specifically, it returns *length* number of characters starting from *start* position. The *length* argument is optional. If it is omitted, the substring starting from *start* position until the end of *string* is returned.

# Example

```
```php
<?php

$a = "Hello Athena";

echo substr ($a, 6, 3);        //Outputs: Ath
echo "\n";
echo substr ($a, 7);           //Outputs: thena
?>
```
```