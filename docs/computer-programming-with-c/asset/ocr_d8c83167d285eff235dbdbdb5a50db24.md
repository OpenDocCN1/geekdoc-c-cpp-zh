```
printf("\n");
}
}
```

# Output

```
Enter the number of rows: 4
*   *   *   *   *   *   *
*   *   *           *   *   *
*   *                   *   *
*                           *
```

| Trace stage | Details shown |
|---|---|
| Initial value of variable i | i = 0 |
| Condition of the outer loop | i <= 3; assume value of x is 4, hence x - 1 = 3 |
| Left loop prints i - 1 stars | Inner loop uses j to print the left-side stars |
| Middle loop prints 2*i spaces | Inner loop uses j to print spaces |
| Right loop prints i - 1 stars | Inner loop uses j to print the right-side stars |
| Position the cursor on the new line | `printf("\n");` is executed as required |
| Increment variable i | `i++` is executed; the next value of i is shown |
| Execution values | i = 0, i = 1, i = 2, i = 3; at i = 4, the outer loop terminates because the condition is not satisfied |

**Figure 5.20:** Execution trace to generate the given symmetric pattern