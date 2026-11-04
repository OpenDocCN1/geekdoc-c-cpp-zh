# Alternative solution

This time let's use decrementing outer for-loop using row variable (5 to 1) and try to determine the logical condition in order to position the numeric character(s) in our row by column picture format.

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 5 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 5 | 5 | 5 | 5 | 5 |

row =5 , 1 <=Col <= 5 (print upper_limit=5)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 4 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 4 | 4 | 4 | 4 |  |

row = 4 , (1 <=Col <= 4) (print upper_limit=4)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 3 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 3 | 3 | 3 |  |  |

row = 3 , (1 <=Col <= 3) (print upper_limit=3)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 2 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 2 | 2 |  |  |  |

row = 2 , (1 <=Col <= 2) (print upper_limit=2)

|  | 1 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|---|
| row | 1 |  |  |  |  |
| col | 1 | 2 | 3 | 4 | 5 |
| output | 1 |  |  |  |  |

row = 1 , (1 <=Col <= 1) (print upper_limit=1)

| Column level Repetitive Action |  |  | Expected Output |
|---|---|---|---|
| row | lower_limit <=col<= upper_limit |  |  |
|  | lower_limit | upper_limit |  |
| 5 | 1 | 5 | 5 5 5 5 5 |
| 4 | 1 | 4 | 4 4 4 4 |
| 3 | 1 | 3 | 3 3 3 |
| 2 | 1 | 2 | 2 2 |
| 1 | 1 | 1 | 1 |

The numeric output will be the value of row variable printed that many times equals the upper_limit of row variable.