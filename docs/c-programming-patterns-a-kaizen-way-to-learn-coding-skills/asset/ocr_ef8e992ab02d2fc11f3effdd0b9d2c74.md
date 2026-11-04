In the logical condition (row+col ==6) &&(row<=3 && col>=3) , every (row, col) value pair in (row+col==6) are given by (5, 1), (4, 2), (3, 3), (2, 4), (1, 5).

| (row, col) value pair | row value | col value |
|---|---|---|
| (1, 5) | 1 | 5 |
| (2, 4) | 2 | 4 |
| (3, 3) | 3 | 3 |
| (4, 2) | 4 | 2 |
| (5, 1) | 5 | 1 |

Every row value is unique within their group of values and is similar with the case for col values too. Hence, considering either row value or col value is sufficient. It is not necessary to consider both the values of row and col to apply restriction condition as given by &&(row <=3 && col>=3).

So part of total logical condition which is given by (row <=3 && col>=3), considering either row<=3 or col>=3 is enough. This could be further given by

```
((row+col ==6 && row <=3 ) or ((row+col ==6 && col>=3 ).
```

We can rewrite the actual logical condition as;

```
(col==1)||(col==5)||
((row==col)&& row <=3)||
( row+col ==6 && row <=3 )
```

Please notice the restriction condition &&row <=3 is same for both logical condition expressions.

We can can again rewrite logical condition in more compact form and can be given as follows:

```
(col==1)||(col==5)||
( ( ( row==col)||( row+col ==6) ) && row<=3 )
```