Be careful about one thing though: only variables can be passed by reference. You cannot pass by reference a constant value or an expression, as shown here.

```
```php
<?php

    function f1(&$b) {
        $b++;
    }

    $x = 9;
    f1($x);             //This works fine!

    f1(10);             //This produces an error!

    f1($x + 1);         //This produces also an error!

?>
```
```

The second and third calls to the function produce an error. This happens because when the flow of execution returns from the procedure to the main code, the value of variable $b must be assigned back to an argument in the actual argument list. Obviously, this cannot be done when the argument is either a constant value or an expression.

So, as you have probably realized, passing values by reference can provide an indirect way for a subprogram to “return” values. In the next example, the function div_mod() divides variable $a by variable $b and finds their integer quotient and their integer remainder. If all goes well, it returns true; otherwise, it returns false. Moreover, through the two arguments $int_quotient and $int_remainder, the function also indirectly returns the calculated quotient and the calculated remainder.

```
```php
<?php

    function div_mod($a, $b, &$int_quotient, &$int_remainder) {
        $return_value = true;
        if ($b == 0) {
            $return_value = false;
        }
        else {
            $int_quotient = intval($a / $b);
            $int_remainder = $a % $b;
        }
        return $return_value;
    }

    $val1 = trim(fgets(STDIN));
```
```