If we take values of row variable starting from 0 instead of 1, then it will help us to generalise the **upper_limit**. Let try to generalise both of these using variable **row**.

If we observe, we try to generalise lower_limit & upper_limit of printing spaces column using **row** variable. With using simple maths we can alter lower_limit & upper_limit so that part of expression which is following a numeric pattern may match with the numeric pattern of **row** variable.

**Row level Repetitive Action**

| row | Print numbers lower_limit | Print numbers upper_limit | Print spaces lower_limit | Print spaces upper_limit | Print numbers lower_limit | Print numbers upper_limit | Output |
|---:|---|---|---|---|---|---|---|
| 1 | 1 | totalRows - 1 | 0 | -1 | 6 | 9 | 4, 3, 2, 1 |
| 2 | 1 | totalRows - 1 | totalRows - 0 | totalRows + 0 | 6 | 9 | 4, 3, 2, 1 |
| 3 | 1 | totalRows - 2 | totalRows - 1 | totalRows + 1 | 7 | 9 | 3, 2, 1 |
| 4 | 1 | totalRows - 3 | totalRows - 2 | totalRows + 2 | 8 | 9 | 2, 1 |
| 5 | 1 | totalRows - 4 | totalRows - 3 | totalRows + 3 | 9 | 9 | 1 |

*Column level Repetitive Action: 1 <=col<=9*

**Row level Repetitive Action**

| row | Print numbers lower_limit | Print numbers upper_limit | Print spaces lower_limit | Print spaces upper_limit | Print numbers lower_limit | Print numbers upper_limit |
|---:|---|---|---|---|---|---|
| 0 | 1 | totalRows - 1 |  |  | 6 | 9 |
| 1 | 1 | totalRows - 1 | totalRows - 0 | totalRows + 0 | 6 | 9 |
| 2 | 1 | totalRows - 2 | totalRows - 1 | totalRows + 1 | 7 | 9 |
| 3 | 1 | totalRows - 3 | totalRows - 2 | totalRows + 2 | 8 | 9 |
| 4 | 1 | totalRows - 4 | totalRows - 3 | totalRows + 3 | 9 | 9 |

*Column level Repetitive Action: 1 <=col<=9*

**Row level Repetitive Action**

| row | Print numbers lower_limit | Print numbers upper_limit | Print spaces lower_limit | Print spaces upper_limit | Print numbers lower_limit | Print numbers upper_limit |
|---:|---|---|---|---|---|---|
| 0 | 1 | totalRows - 1 | 0 | -1 | 6 | 9 |
| 1 | 1 | totalRows - row | totalRows - 1 + 1 | totalRows + 1 - 1 | 6 | 9 |
| 2 | 1 | totalRows - row | totalRows - 2 + 1 | totalRows + 2 - 1 | 7 | 9 |
| 3 | 1 | totalRows - row | totalRows - 3 + 1 | totalRows + 3 - 1 | 8 | 9 |
| 4 | 1 | totalRows - row | totalRows - 4 + 1 | totalRows + 4 - 1 | 9 | 9 |

*Column level Repetitive Action: 1 <=col<=9*