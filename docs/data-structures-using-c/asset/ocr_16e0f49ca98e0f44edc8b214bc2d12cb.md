![](bbox=[0.2, 0.1, 0.89, 0.31])

The cylinder-surface index consists of a cylinder index and several surface indices. If the file requires 1 through C cylinders, then there are C entries in the cylinder index. There is one entry corresponding to the largest key value in each cylinder. For each cylinder, there is a surface index. If the disk has S usable surfaces, then each surface index has S entries. The total number of surface index entries is C x S. For example, consider Table 13.2.

| Emp. no. | Emp. name | Cylinder | Surface |
|---|---|---|---|
| 1 | Abolee | 1 | 1 |
| 2 | Anand | 1 | 1 |
| 3 | Amit | 1 | 2 |
| 4 | Amol | 1 | 2 |
| 5 | Rohit | 2 | 1 |
| 6 | Santosh | 2 | 1 |
| 7 | Saurabh | 2 | 2 |
| 8 | Shila | 2 | 2 |

Let there be two surfaces and two records per track. The file is organized sequentially on the field 'Emp. name'. The corresponding cylinder index is given in Table 13.3.

| Cylinder | Highest key value |
|---|---|
| 1 | Amol |
| 2 | Shila |

The surface index for cylinder 1 is the surface highest key value: Anand, Amol. The surface index for cylinder 2 is the surface highest key value: Santosh, Shila.