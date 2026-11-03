```
2 2222 3000
2 2222 4465.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
3 3333 2000
3 3333 3007.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
4 4444 1000
4 4444 1500.00
Enter level, job number, and basic pay
Enter 0 (zero) for level to END
0
END OF THE PROGRAM
```

Fig. 6.15 Pay-bill calculations

# Review Questions and Exercises

# 6.1 Determine whether the following are true or false:

+   (a) When if statements are nested, the last else gets associated with the nearest if without an else.
+   (b) One if can have more than one else clause.
+   (c) A switch statement can always be replaced by a series of if…else statements.
+   (d) A switch expression can be of any type.
+   (e) A program stops its execution when a break statement is encountered.

6.2 In what ways does a switch statement differ from an if statement?

6.3 Find errors, if any, in each of the following segments:
(a) if (x + y = z && y > 0)
    printf(" ");
(b) if (code > 1);
    a = b + c
    else
    a = 0
(c) if (p < 0) ; (q < 0)
    printf("sign is negative");
6.4 The following is a segment of a program:
    x = 1;
    y = 1;
    if(n > 0)
    x = x + 1;
    y = y - 1;
    printf("%d %d", x, y);