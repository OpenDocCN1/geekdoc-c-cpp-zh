| To | Do this |
|---|---|
| Declare a jagged array variable | Declare the variable as an array of arrays. You can initialize each nested array to have a different length. For example, use the following to create a jagged array called items and initialize each nested array: |

```
int[][] items;
items = new int[4][];
items[0] = new int[3];
items[1] = new int[10];
items[2] = new int[40];
items[3] = new int[25];
```