```
```
switch (expression)
{
    case const-expr:
        set of statements;
        break;
    case const-expr:
        set of statements;
        break;
    ...
    default:
        set of statements;
}
```
```

The expression tested, as mentioned above, must be of an integral type, typically an integer or a character. The branching to a set of statements occurs in the case clause portion of the switch statement. The constant expression (const-expr) in the case clause is compared with the opening expression. If the comparison is true, the set of statements inside that clause are executed and then control is transferred out of the switch statement due to the break statement. If the comparison is false, control falls to the next case clause. If none of the case clauses are executed and a default clause is present, the statements inside the default clause are executed.

Some examples will probably clear up any misconceptions you have about how the switch statement works. In this first example, a letter grade is entered and the possible numeric range of the letter grade is displayed: