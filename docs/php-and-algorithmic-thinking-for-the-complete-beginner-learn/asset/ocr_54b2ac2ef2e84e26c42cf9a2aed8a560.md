| 2 | display_abs ($a) | | -5 |
|---|---|---|---|
| 3 | if ($n < 0) | This evaluates to true | |
| 4 | $n = (-1) * $n | | 5 |
| 5 | echo $n | Value 5 is displayed | |
| 6 | echo $a | Value –5 is displayed | |

**Notice:** Please note that at step 5 the variable `$n` of the procedure contains the value 5 but when the flow of execution returns to the main code at step 6, the variable `$a` of the main code contains the value -5. Actually, the value of variable `$a` of the main code had never changed!

# ## Exercise 40.4-2 _A Simple Currency Converter_

Do the following:

+   i. Write a procedure named `display_menu()` that displays the following menu.
+   
+   1. Convert USD to Euro (EUR)
+   2. Convert Euro (EUR) to USD
+   3. Exit

+   ii. Using the procedure `display_menu()` cited above, write a PHP script that displays the previously mentioned menu and prompts the user to enter a choice (of 1, 2, or 3) and an amount of money. The script should then calculate and display the required value. The process should repeat as many times as the user wishes. It is given that $1 = 0.72 EUR (€).

# ### Solution

The solution is very simple and needs no further explanation.

```
```php
<?php
function display_menu() {
    echo "1. Convert USD to Euro (EUR)\n";
    echo "2. Convert Euro (EUR) to USD\n";
    echo "3. Exit\n";
    echo "----------------------------------\n";
    echo "Enter a choice: ";
}

do {
    display_menu();
    $choice = trim(fgets(STDIN));
```
```