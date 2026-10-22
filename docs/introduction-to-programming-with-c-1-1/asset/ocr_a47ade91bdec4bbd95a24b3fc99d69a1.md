```
}

getch();
return(0);
}
```

Output

```
Enter your marks

96

YOUR GRADE : A

Enter your marks

75

YOUR GRADE : B

Enter your marks

60

YOUR GRADE : C

Enter your marks

35

YOUR GRADE : Failed
```

# Cascaded if..else

A cascading if-else is a composite of if-else statements where the false path of outer if statement is a nested if-else statement. The nesting can continue to several levels.

```
if ( expression )
statement

else

    if (expression )
    statement

    else

    if ( expression )
    statement

    else
```