columns.

| NAME | SALARIES |
|---|---:|
| John | 5,000 |
| Mary | 7,000 |
| Jennifer | 9,000 |
| Mark | 10,000 |
| Adam | 7,000 |

If you would like to remove salaries that are 7,000, then you simply have to use the below:

```
SQL > DELETE FROM EMPLOYEES
    WHERE SALARIES = 7,000
SQL > COMMIT;
```

Now, as mentioned before, if you would like the next transaction to begin after the execution of the current one, then your statement will look something like this:

```
SQL > DELETE FROM EMPLOYEES
    WHERE SALARIES = 7,000
SQL > COMMIT AND CHAIN;
```

# Rollback

Human error is a permanent fixture in any process. For this reason, if you find a situation that calls for a roll back, then this statement gives you the power to commit such an action.

By using ROLLBACK, you will undo the statements you have done so far, either bringing them back to a specific savepoint – if you had established such a savepoint – or sending them to the beginning of the transaction.