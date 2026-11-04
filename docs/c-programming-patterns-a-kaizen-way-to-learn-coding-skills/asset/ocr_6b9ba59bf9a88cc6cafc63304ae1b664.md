Let's try to simplify program further by simplifying the <u>if-conditions</u> and loop-condition <u>expressions</u>.

For example, let's analyse the following expression when **col** is a variable which <u>**starts from value 0.**</u>

When variable col=5,6,..., will have the values, which means the logical condition to cover these values can be expressed as **col >= ( 4 + 1 ) or col > 4**, both means the same.

Similarly,

The variable **col=0,1,2,3** when contains the values, means col <= ( 4 – 1 ) or col < 4 ,both means the same.

In the same way the <u>**if-conditions**</u> and loop-condition <u>*expressions*</u> can be simplified.

The <u>**if-condition**</u> gives the minimum limit, a starting point for which program will start printing start("*") character(s) till the maximum value of variable col given by the <u>**loop-condition**</u>.

Let's consider;

+   - **colMin →** variable *type of integer* to store integer value of column , a starting point from which program will start printing start("*") character.
+   - **colMax →** variable *type of integer* to store integer value of column , a maximum value till program will stop printing star("*") character(s).

| Variable : row | if-conditions | |
|---|---|---|
| | Variable : colMin | |
| | **default** | **1** |
| row <= totalRows | col >= ( totalRows – row + 1 ) | col > ( totalRows – row ) |
| row > totalRows | col >= ( row – totalRows + 1 ) | col > ( row – totalRows ) |

| Variable : row | loop-conditions | |
|---|---|---|
| | Variable : colMax | |
| | **default** | **1** |
| row <= totalRows | col <= ( totalRows + row – 1 ) | col < ( totalRows + row ) |
| row > totalRows | col <= ( 3 + totalRows – row – 1 ) | col < ( 3 + totalRows – row ) |

Using variables **colMin & colMax** we can merge the two inner-loops by dynamically assigning these expression to these variables.