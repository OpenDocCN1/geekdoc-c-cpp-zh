```
```cpp
if (grade >= 70)
{
    passFail = true;
    bonus += 5;
}
```
```

Starting the block this way is a stylistic convention you may follow if you want to, but whatever style you choose, you should be consistent and use the same style all the time.

An if statement can be placed inside an if statement. This is called a nested if statement. Here is an example:

```
```cpp
int num1, num2, num3;
cout << "Enter three numbers: ";
cin >> num1 >> num2 >> num3;
if (num1 > num2)
    if (num1 > num3)
        cout << "The largest number is " << num1
             << endl;
```
```

If the first condition is true, then the second if statement nested inside the first if statement is executed.

When you want to use an else statement with a nested if statement, the else statement is always paired with the closest if statement. For example: