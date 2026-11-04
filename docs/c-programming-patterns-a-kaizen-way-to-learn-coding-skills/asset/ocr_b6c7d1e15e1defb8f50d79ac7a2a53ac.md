We can now define column level **decrementing for-loop**.

It starts at value of variable **row** and will repeatedly decrease till **col** value becomes **1**.

# ***Elements of Column level decrementing for-loop***

|  |  |
|---|---|
| *max_val* | row |
| *min_val* | 1 |
| *variable_name* | col |
| **Loop condition** | col >=1 |
| statement(s) | print("*"); |

# **ROW LEVEL REPETITIVE ACTION**

Outer **decrementing for-loop** starts at <u>totalRows</u> & will repeatedly decrease till row value becomes 1.

# ***Elements Of Row Level decrementing for-loop***

|  |  |
|---|---|
| *max_val* | totalRows |
| *min_val* | 1 |
| *variable_name* | row |
| **Loop condition** | row >=1 |
| statement(s) | **Column level for-loop**<br>// Move cursor to the next row<br>print("\n"); |

Hence we got everything related to the nested ***for-loop***.

![](bbox=[0.45, 0.45, 0.95, 0.95])