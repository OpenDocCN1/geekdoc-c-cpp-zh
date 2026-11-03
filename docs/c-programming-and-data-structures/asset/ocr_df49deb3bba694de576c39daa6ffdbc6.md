```
if (A>B)
{
    if (A<C)
        printf("%f\n", A);
    else
        printf("%f\n", C);
}
else
{
    if (C>B)
        printf("%f\n", C);
    else
        printf("%f\n", B);
}
```

Output
Enter three values
23445 67379 88843
Largest value is 88843.000000

Fig. 2.8 Selecting the largest of three numbers

# Dangling Else Problem

One of the classic problems encountered when we start using nested if....else statements is the dangling else. This occurs when a matching else is not available for an if. The answer to this problem is very simple. Always match an else to the most recent unmatched if in the current block. In some cases, it is possible that the false condition is not required. In such situations, else statement may be omitted

"else is always paired with the most recent unpaired if"

# 2.6 THE ELSE IF LADDER

There is another way of putting ifs together when multipath decisions are involved. A multipath decision is a chain of ifs in which the statement associated with each else is an if. It takes the following general form:

```
if ( condition 1)
    statement-1;
else if ( condition 2)
    statement-2;
else if ( condition 3)
    statement-3;
else if ( condition n)
    statement-n;
else
    default-statement;
statement-x;
```

This construct is known as the else if ladder. The conditions are evaluated from the top (of the ladder), downwards. As soon as a true condition is found, the statement associated with it is executed and the control