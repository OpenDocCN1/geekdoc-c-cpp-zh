| Possible Observation | Reason why this may occur? |
| :--- | :--- |
| No problem, program works as expected. | Going beyond the limits of the array and into memory that is NOT reserved for the purpose of the array MAY NOT be reserved for any other purpose. |
| Program executes, but results are unexpected. | Going beyond the limits of the array and into memory that is NOT reserved for the purpose of the array MAY be reserved for any other purpose and multiple edits to the same memory may leave an unexpected value being stored. |
| Program crashes. | Going beyond the limits of the array and attempting to access memory that DOES NOT exist or that the program does not have the ability to access. |

# Examples of exceeding the defined limits of an array

```
int x[5] = {8, 4, 5, 2, 3};
```

| 8 | 4 | 5 | 2 | 3 |
| 0 | 1 | 2 | 3 | 4 |

| 8 | 4 | 5 | 2 | 3 |
| 0 | 1 | 2 | 3 | 4 |

| 8 | 4 | 5 | 2 | 3 |
| 0 | 1 | 2 | 3 | 4 |