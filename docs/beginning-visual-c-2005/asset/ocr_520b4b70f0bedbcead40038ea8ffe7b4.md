# The do-while Loop

The do-while loop is similar to the while loop in that the loop continues as long as the specified loop condition remains true. The main difference is that the condition is checked at the end of the loop — which contrasts with the while loop and the for loop where the condition is checked at the beginning of the loop. Consequently, the do-while loop statement is always executed at least once. The general form of the do-while loop is:

```
do
{
    loop_statements;
}while(condition);
```

The logic of this form of loop is shown in Figure 3-6.

![](bbox=[0.15, 0.35, 0.78, 0.65])

Figure 3-6

You could replace the while loop in the last version of the program to calculate an average with a do-while loop:

```
do
{
    cout << endl
        << "Enter a value: ";
    cin >> value;                // Read a value
    ++i;                         // Increment count
    sum += value;                // Add current input to total

    cout << "Do you want to enter another value (enter n to end)?";
    cin >> indicator;            // Read indicator
} while((indicator == 'y') || (indicator == 'Y'));
```