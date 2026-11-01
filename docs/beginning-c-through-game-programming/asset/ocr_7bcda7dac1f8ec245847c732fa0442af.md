inside another, it's called nesting. In the following code, the if statement that begins if (score >= 1000) is nested inside the if statement that begins if (score > 500).

```
if (score >= 500)
{
    cout << "You scored 500 or more. Nice.\n\n";
    
    if (score >= 1000)
    {
        cout << "You scored 1000 or more. Impressive!\n";
    }
}
```

Because score is greater than 500, the program enters the statement block and displays the message, "You scored 500 or more. Nice." Then, in the inner if statement, the program compares score to 1000. Because score is greater than or equal to 1000, the program displays the message, "You scored 1000 or more. Impressive!"

# Hint

You can nest as many levels as you want. However, if you nest code too deeply, it gets hard to read. In general, you should try to limit your nesting to a few levels at most.

# USING THE ELSE CLAUSE

You can add an else clause to an if statement to provide code that will only be executed if the tested expression is false. Here's the form of an if statement that includes an else clause:

```
if (expression)
    statement1;
else
    statement2;
```

If expression is true, statement1 is executed. Then the program skips statement2 and executes the statement following the if suite. If expression is false, statement1 is skipped and statement2 is executed. After statement2 completes, the program executes the statement following the if suite.