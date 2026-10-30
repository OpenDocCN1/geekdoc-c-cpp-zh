# TABLE 8.7: Car Selection Data

| Cars | Cost ($1000) | MPG City | MPG Highway | Performance | Interior & Style | Safety | Reliability |
|---|---:|---:|---:|---:|---:|---:|---:|
| Prius | 27.8 | 44 | 40 | 7.5 | 8.7 | 9.4 | 3 |
| Fusion | 28.5 | 47 | 47 | 8.4 | 8.1 | 9.6 | 4 |
| Volt | 38.7 | 35 | 40 | 8.2 | 6.3 | 9.6 | 3 |
| Camry | 25.5 | 43 | 39 | 7.8 | 7.5 | 9.4 | 5 |
| Sonata | 27.5 | 36 | 40 | 7.6 | 8.3 | 9.6 | 5 |
| Leaf | 36.2 | 40 | 40 | 8.1 | 8.0 | 9.4 | 3 |

Initially, we assume all criteria are weighted equally to obtain a baseline ranking. Even though the different criteria values are relatively close, let’s normalize the data for illustration. There are three typical methods to use:

$m_{ij} \rightarrow \frac{m_{ij}}{M_j},\quad m_{ij} \rightarrow \frac{m_{ij}-m_j}{M_j-m_j},\quad m_{ij} \rightarrow \operatorname{rank}_j(m_{ij})$

where $M_j$ and $m_j$ are the maximum and minimum values in the $j$th column, and $\operatorname{rank}_j$ is the rank order of the $j$th column. Our SAW program from the PSMv2 package uses the first method.

We’ll exclude the cost data from our first baseline ranking since larger cost is worse, whereas all the other data has larger is better. SAW requires consistent criteria ranking.

```
[-] CarModel := Vector[row]([Prius, Fusion, Volt, Camry, Sonata, Leaf]);

[-] CarData :=
    [  44   40   7.5  8.7  9.4  3
       47   47   8.4  8.1  9.6  4
       35   40   8.2  6.3  9.6  3
       43   39   7.8  7.5  9.4  5
       36   40   7.6  8.3  9.6  5
     40   40   8.1  8.0  9.4  3 ];

    Price := (27.8, 28.5, 38.7, 25.5, 27.5, 36.2);

[-] equalWeights := (1/6$6);
```

The SAW function will return a matrix of rankings. The first row is a raw ranking, the second row is normalized so the largest ranking is 1. We’ll apply fnormal to the rankings and add a legend to make it easier to read the results.