```
$a = "          Zeus!";

$b = ltrim($a);

echo "Hello ", $b;        //Outputs: Hello Zeus!
?>
```

# Right trimming

```
rtrim (string)
```

This removes any whitespace characters from the end of string.

# Example

# file_14.4b.php

```
<?php
$a = "Hello          ";

$b = rtrim($a);

echo $b, " Hera!";        //Outputs: Hello Hera!
?>
```

# Left & Right trimming

```
trim (string)
```

This removes any whitespace characters from both the beginning and the end of string.

# Example

# file_14.4c.php

```
<?php
$a = "      Hello      ";

$b = trim($a);

echo $b, " Poseidon!";        //Outputs: Hello Poseidon!
?>
```

# String replacement

```
str_replace (search, replace, subject)
```

This searches in subject and replaces all occurrences of the search string with the replace string.

# Example

# file_14.4d.php

```
<?php
```