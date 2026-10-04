# Selection Structures

If break statements are omitted, all cases following the matching case value, including the default case, are executed.
When writing a switch statement, you can use multiple case values to refer to the same set of statements; the default keyword is optional. For example, take a look at the:

```
switch (number)
{
  case 1:
    cout << "Have a Good Morning\n";
    break;
  case 2:
    cout << "Have a Happy Day\n";
    break;
  case 3:
  case 4:
  case 5:
    cout << "Have a Nice Evening\n";
}
```

If the value stored in the variable number is 1, the message Have a Good Morning is displayed. Similarly, if the value of number is 2, the second message is displayed. Finally, if the value of number is 3, 4, or 5, the last message is displayed. Because the statement to be executed is "stacked together", all cases are executed. For example, because there's no default keyword, no message is printed if the value of number is not any of the listed case values. Although listing case values in increasing order is a good programming practice, it's not required by the switch statement. A switch statement can have any number of case values, in any order; only the values you're testing for must be listed.

Program 4.7 uses a switch statement to select the arithmetic operation (addition, multiplication, or division) to perform on two numbers, depending on the value of the select variable.
In the two sample runs, the resulting display clearly identifies the case that was selected:

and

```
Please type in two numbers: 12 3
Enter a select code:
1 for addition
2 for multiplication
3 for division : 3
The first number divided by the second is 4
```