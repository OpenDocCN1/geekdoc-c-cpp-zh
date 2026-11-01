```
if (score >=1000)
{
    cout << "You scored 1000 or more. Impressive!\n";
}
else if (score >=500)
{
    cout << "You scored 500 or more. Nice.\n";
}
else if (score >=250)
{
    cout << "You scored 250 or more. Decent.\n";
}
else
{
    cout << "You scored less than 250. Nothing to brag about.\n";
}

return 0;
}
```

# Creating a Sequence of if Statements with else Clauses

You've seen the first part of this sequence twice already, and it works just the same this time around. If score is greater than or equal to 1000, the message, “You scored 1000 or more. Impressive!” is displayed and the computer branches to the return statement.

```
if (score >=1000)
```

However, if the expression is false, then we know that score is less than 1000 and the computer evaluates the next expression in the sequence:

```
else if (score >=500)
```

If score is greater than or equal to 500, the message, “You scored 500 or more. Nice.” is displayed and the computer branches to the return statement. However, if that expression is false, then we know that score is less than 500 and the computer evaluates the next expression in the sequence:

```
else if (score >=250)
```

If score is greater than or equal to 250, the message, “You scored 250 or more. Decent.” is displayed and the computer branches to the return statement.