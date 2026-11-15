# PRACTICE!

In Problems 1 through 7, draw a flowchart to perform the steps indicated. Then give the corresponding C statements. Assume that the variables have been declared and have reasonable values.

+   1. If time is greater than 15.0, increment time by 1.0.
+   2. When the square root of poly is less than 0.5, print the value of poly.
+   3. If the difference between volt_1 and volt_2 is larger than 10.0, print the values of volt_1 and volt_2.
+   4. If the value of den is less than 0.05, set result to zero; otherwise, set result equal to num divided by den.
+   5. If the natural logarithm of x is greater than or equal to 3, set time equal to zero and decrement count.
+   6. If dist is less than 50.0 and time is greater than 10.0, increment time by 2; otherwise, increment time by 2.5.
+   7. If dist is greater than or equal to 100.0, increment time by 2.0. If dist is between 50 and 100, increment time by 1. Otherwise, increment time by 0.5.

# switch Statement

The switch statement is used for multiple-selection decision making. In particular, it is often used to replace nested if/else statements. Before giving the general discussion of the switch statement, we present a simple example that uses nested if/else statements and then an equivalent solution that uses the switch statement.

Suppose that we have a temperature reading from a sensor inside a large piece of machinery. We want to print a message on the control screen to inform the operator of the temperature status. If the status code is 10, the temperature is too hot and the equipment should be turned off; if the status code is 11, the operator should check the temperature every 5 minutes; if the status code is 13, the operator should turn on the circulating fan; for all other status codes, the equipment is operating in a normal mode. The correct message could be printed with the following set of nested if/else statements:

```
if (code == 10)
    printf("Too hot - turn equipment off \n");
else
{
    if (code == 11)
        printf("Caution - recheck in 5 minutes \n");
    else
    {
        if (code == 13)
            printf("Turn on circulating fan \n");
        else
            printf("Normal mode of operation \n");
    }
}
```