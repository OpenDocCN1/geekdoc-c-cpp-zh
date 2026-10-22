```
{
    if (ch != '"' && ch != '\'')
        charcount++;
}
printf("There are %d non-quote characters.\n", charcount);

return 0;
}
```

The following is a sample run:

```
I didn't read the "I'm a Programming Fool" best seller.
There are 50 non-quote characters.
```

The action begins as the program reads a character and checks to see whether it is a period, because the period marks the end of a sentence. Next comes something new, a statement using the logical AND operator, &&. You can translate the if statement as, "If the character is not a double quote AND if it is not a single quote, increase charcount by 1."

Both conditions must be true if the whole expression is to be true. The logical operators have a lower precedence than the relational operators, so it is not necessary to use additional parentheses to group the subexpressions.

C has three logical operators:

| Operator | Meaning |
|---|---|
| && | and |
| || | or |
| ! | not |

Suppose exp1 and exp2 are two simple relational expressions, such as cat > rat and debt == 1000. Then you can state the following:

+   - exp1 && exp2 is true only if both exp1 and exp2 are true.
+   - exp1 || exp2 is true if either exp1 or exp2 is true or if both are true.
+   - !exp1 is true if exp1 is false, and it's false if exp1 is true.

Here are some concrete examples:

5 > 2 && 4 > 7 is false because only one subexpression is true.
5 > 2 || 4 > 7 is true because at least one of the subexpressions is true.
!(4 > 7) is true because 4 is not greater than 7.