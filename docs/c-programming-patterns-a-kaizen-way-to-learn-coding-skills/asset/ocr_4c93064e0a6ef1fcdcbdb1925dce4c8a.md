Further, simplifying upper_limit by subtracting 1 as shown in the following;

| Column level Repetitive Action |  |  |  |  |
|---|---|---|---|---|
| *row* | *upper_limit >=col>= lower_limit* |  |  |  |
|  | lower_limit | upper_limit |  |  |
| 1 - 1 | 0 | 1 | (totalRows + 1) – row – 1 | (totalRows – row) |
| 2 - 1 | 1 | 1 | (totalRows + 1) – row – 1 | (totalRows – row) |
| 3 - 1 | 2 | 1 | (totalRows + 1) – row – 1 | (totalRows – row) |
| 4 - 1 | 3 | 1 | (totalRows + 1) – row – 1 | (totalRows – row) |
| 5 - 1 | 4 | 1 | (totalRows + 1) – row – 1 | (totalRows – row) |

Hence, our improved if-condition will be,

| if-condition | *upper_limit >=col>= lower_limit* |
|---|---|
| **Mathematical expression** | col <= ( ( totalRows – row ) |
| Syntax | `if( col <= (totalRows – row) )` |

The modification can be easily expressed in the flow-chart.

![](bbox=[0.153, 0.477, 0.816, 0.826])