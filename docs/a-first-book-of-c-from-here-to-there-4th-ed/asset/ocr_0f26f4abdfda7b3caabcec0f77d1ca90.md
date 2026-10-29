As a general rule, the continue statement is less useful than the break statement, but it’s convenient for skipping over data that shouldn’t be processed while remaining in a loop. For example, invalid grades are simply ignored in the following section of code, and only valid grades are added to the total:

```
while (count < 30)
{
cout << "Enter a grade: ";
cin >> grade;
if(grade < 0 || grade > 100)
    continue;
total = total + grade;
count++;
}
```

# The Null Statement

All statements must be terminated by a semicolon. A semicolon with nothing preceding it is also a valid statement, called the null statement, as shown:

```
;
```

It’s a do-nothing statement used where a statement is required syntactically, but no action is called for. Typically, null statements are used with while or for statements. Program 5.9c in Section 5.3 shows an example of a for statement using a null statement.

# EXERCISES 5.2

+   1. (Modify) Rewrite Program 5.6 to compute the total of eight numbers.

+   2. (Modify) Rewrite Program 5.6 to display this prompt:
+   
+   Please type in the total number of data values to be added:
+   
+   In response to this prompt, the program should accept a user-entered number, and then use it to control the number of times the while loop is executed. So if the user enters 5 in response to the prompt, the program should request the input of five numbers and display the total after five numbers have been entered.

+   3. (Modify) Rewrite Program 5.7 to compute the average of 10 numbers.

> 1 Although this section of code illustrates the flow of control the continue statement provides, it’s not the preferred way of achieving the correct result. Instead of using an if statement and a continue statement to exclude invalid data, a better method is including valid data with these statements:
> if (grade >= 0 && grade <= 100)
> {
>     total = total + grade;
>     count++;
> }