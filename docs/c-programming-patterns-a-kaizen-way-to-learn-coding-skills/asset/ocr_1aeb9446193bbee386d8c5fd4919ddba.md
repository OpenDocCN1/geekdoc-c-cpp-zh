```
1 2 3 4 5 4 3 2 1
1 2 3 4   4 3 2 1
1 2 3       3 2 1
1 2           2 1
1               1
```

# NumberPatternFF

# Tabular representation

|  | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 | Col=6 | Col=7 | Col=8 | Col=9 |
|---|---|---|---|---|---|---|---|---|---|
| Row=1 | 1 | 2 | 3 | 4 | 5 | 4 | 3 | 2 | 1 |
| Row=2 | 1 | 2 | 3 | 4 | space | 4 | 3 | 2 | 1 |
| Row=3 | 1 | 2 | 3 | space | space | space | 3 | 2 | 1 |
| Row=4 | 1 | 2 | space | space | space | space | space | 2 | 1 |
| Row=5 | 1 | space | space | space | space | space | space | space | 1 |

# (Row, Col) value pairs representation.

|  | Col=1 | Col=2 | Col=3 | Col=4 | Col=5 | Col=6 | Col=7 | Col=8 | Col=9 |
|---|---|---|---|---|---|---|---|---|---|
| Row=1 | (1,1)<br>1 | (1,2)<br>2 | (1,3)<br>3 | (1,4)<br>4 | (1,5)<br>5 | (1,6)<br>4 | (1,7)<br>3 | (1,8)<br>2 | (1,9)<br>1 |
| Row=2 | (2,1)<br>1 | (2,2)<br>2 | (2,3)<br>3 | (2,4)<br>4 | **2,5**<br>space | (2,6)<br>4 | (2,7)<br>3 | (2,8)<br>2 | (2,9)<br>1 |
| Row=3 | (3,1)<br>1 | (3,2)<br>2 | (3,3)<br>3 | **3,4**<br>space | **3,5**<br>space | **3,6**<br>space | (3,7)<br>3 | (3,8)<br>2 | (3,9)<br>1 |
| Row=4 | (4,1)<br>1 | (4,2)<br>2 | **4,3**<br>space | **4,4**<br>space | **4,5**<br>space | **4,6**<br>space | **4,7**<br>space | (4,8)<br>2 | (4,9)<br>1 |
| Row=5 | (5,1)<br>1 | **5,2**<br>space | **5,3**<br>space | **5,4**<br>space | **5,5**<br>space | **5,6**<br>space | **5,7**<br>space | **5,8**<br>space | (5,9)<br>1 |

# Analysis of output

In general, three repetitive action takes place.

+   a) Printing of numbers starting from 1 in incrementing order.
+   
+   b) Printing of spaces
+   
+   c) Printing of numbers in decrementing order and it’s upper limit will start from last updated incremented value.