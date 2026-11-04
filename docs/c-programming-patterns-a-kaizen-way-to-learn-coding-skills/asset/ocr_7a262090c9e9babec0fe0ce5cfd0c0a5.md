Then the logical expression can be expressed in terms of **totalRows** and **count**.

| Row level Repetitive Action ||| Column level Repetitive Action ||||
|---|---|---|---|---|---|---|---|
| Variable : row | Variable : count | Variable : col |||||
|  |  | Printing star character(s) |||||
|  |  | min_val | 2 | max_val | 2 ||
|  |  | default | 5 | default | totalRows + count ||
| 1 | 0 | 5 | totalRows - count | 5 | totalRows + count ||
| 2 | 1 | 4 | totalRows - count | 6 | totalRows + count ||
| 3 | 2 | 3 | totalRows - count | 7 | totalRows + count ||
| 4 | 3 | 2 | totalRows - count | 8 | totalRows + count ||
| 5 | 4 | 1 | totalRows - count | 9 | totalRows + count ||
| 6 | 3 | 2 | totalRows - count | 8 | totalRows + count ||
| 7 | 2 | 3 | totalRows - count | 7 | totalRows + count ||
| 8 | 1 | 4 | totalRows - count | 6 | totalRows + count ||
| 2*totalRows - 1 | 0 | 5 | totalRows - count | 5 | totalRows + count ||

The variable count starts increases by value 1 from the start of the row=1 till the row=**totalRows** **(total number of rows)** and then starts decreases further by value 1 till **(totalRows – 1)** times.

We can deal this using **if-else** conditional statement.

The condition **(col >= (totalRows – count) )** gives starting point from which ***for-loop*** will start printing start("*") character(s) till the maximum value of variable col which is **(totalRows + count)** for every value of row. The **if-condition** can be given using the **comparison and logical operators** for the range of values between **(totalRows – count)** and **(totalRows + count)** as:

```
if ( col >= (totalRows – count) && col <= (totalRows + count) )
```

We already know that;

```
variable col = 1,2,3,4,5 or 1,2,3,4, ...,(totalRows + count) ,
variable row = 1,2,3,...,9 or 1,2,3,...,( 2 * totalRows - 1))
```

**Same expression**

We can eliminate the **logical AND(&&)** condition **( col <= (totalRows + count) )** in the **if-condition**. This **logical AND(&&)** condition already been taken care in the **loop-condition** of the column level inner ***for-loop***. So the if-condition will now reduce to the following:

```
if ( col >= ( totalRows – count) )
```

We can can generalised the non-repeating numeric pattern of the column **max_val** into an expressions. We can now define column level ***for-loop***.

| Elements of Column level for-loop |
|---|---|
| **min_val** | 1 |
| **max_val** | (totalRows + count) |
| **variable_name** | col |
| statement(s) | printf("*"); |