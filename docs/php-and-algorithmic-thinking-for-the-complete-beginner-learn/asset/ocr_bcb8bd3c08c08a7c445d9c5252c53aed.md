```
```php
if ($choice == 3) {
    echo "Bye!";
}
else {
    echo "Enter an amount: ";
    $amount = trim(fgets(STDIN));
    if ($choice == 1) {
        echo $amount, " USD = ", $amount * 0.72, " Euro\n";
    }
    else {
        echo $amount, " Euro = ", $amount / 0.72, " USD\n";
    }
}
} while ($choice != 3);
?>
```
```

# 40.5 Review Questions: True/False

Choose **true** or **false** for each of the following statements.

+   1. In Java, a subprogram that returns no result is known as a void function.
+   2. In PHP, you can call a procedure just by writing its name.
+   3. In a procedure call that is made in main code, within the actual argument list there must be only variables of the main code.
+   4. In a procedure, all formal arguments must have different names.
+   5. An actual argument can be an expression.
+   6. A procedure must always include at least one argument in its formal argument list.
+   7. There is a one-to-one match between the formal and the actual arguments.
+   8. You can call a procedure within a statement.
+   9. When the flow of execution reaches the end of a procedure, the flow of execution continues from where it was before calling the procedure.
+   10. It is possible for a procedure to return no values to the caller.
+   11. It is possible for a procedure to accept no values from the caller.
+   12. A call to a procedure is made differently from a call to a function.
+   13. In the following code fragment

```
```php
function message() {
    echo "Hello Aphrodite!";
}
```
```