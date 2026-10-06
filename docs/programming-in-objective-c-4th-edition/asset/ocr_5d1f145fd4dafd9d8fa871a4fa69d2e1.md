```
break;
}
```

The expression values enclosed within parentheses is successively compared against the values value1, value2, ..., valueen, which must be simple constants or constant expressions. If a case is found whose value is equal to the value of expression, the program statements that follow the case are executed. Note that when more than one program statement is included, they do not have to be enclosed within braces.

The break statement signals the end of a particular case and causes execution of the switch statement to be terminated. Remember to include the break statement at the end of every case. Forgetting to do so for a particular case allows program execution to continue into the next case whenever that case is executed. Sometimes this is done intentionally; if you elect to do so, be sure to insert comments to alert others of your purpose.

The special case called default is executed if the value of expression does not match any of the case values. This is conceptually equivalent to the catchall else used in the previous example. In fact, the general form of the switch statement can be equivalently expressed as an if switch statement, as follows:

```
if ( expression == value1 )
{
    program statement
    program statement
    ...
}
else if ( expression == value2 )
{
    program statement
    program statement
    ...
```