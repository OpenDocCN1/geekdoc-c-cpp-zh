or

```
int x = 0;
while (++x <= 20) {
    if (x % 5 == 0) {
        printf("%d\n", x);
    }
    else {
        printf("%d\t", x);
    }
}
```

```
e) for (int x = 1; x <= 20; ++x) {
    printf("%d", x);
    if (x % 5 == 0) {
        puts("");
    }
    else {
        printf("%s", "\t");
    }
}
```

or

```
for (int x = 1; x <= 20; ++x) {
    if (x % 5 == 0) {
        printf("%d\n", x);
    }
    else {
        printf("%d\t", x);
    }
}
```

+   4.4 a) Error: The semicolon after the while header causes an infinite loop.
+       Correction: Replace the semicolon with a { or remove both the ; and the }.

+   b) Error: Using a floating-point number to control a for iteration statement.
+       Correction: Use an integer, and perform the proper calculation to get the values you desire.

```
for (int y = 1; y != 10; ++y) {
    printf("%f\n", (float) y / 10);
}
```

+   c) Error: Missing break statement in the statements for the first case.
+       Correction: Add a break statement at the end of the statements for the first case. This is not necessarily an error if you want the statement of case 2: to execute every time the case 1: statement executes.